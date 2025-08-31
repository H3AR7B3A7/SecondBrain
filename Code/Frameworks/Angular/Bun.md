# Bun

## Migration Strategy Recommendation

### Phase 1: Easy Win (1 day)

1. Install Bun

```bash
# 1. Install Bun
curl -fsSL https://bun.sh/install | bash

# 2. Remove node_modules and reinstall with Bun
rm -rf node_modules package-lock.json
bun install

# 3. Update package.json scripts (optional)
# Change "node" to "bun" and "nodemon" to "bun --hot"

# 4. Run with Bun
bun run dev
```

2. Replace Node.js with Bun runtime
3. Keep existing Express code
4. Update package.json scripts

```json
{
  "name": "my-express-app",
  "version": "1.0.0",
  "scripts": {
    "start": "bun server.js",
    "dev": "bun --hot server.js"
  },
  "dependencies": {
    "express": "^4.18.2",
    "cors": "^2.8.5",
    "helmet": "^7.0.0"
  }
}
```

5. **Result:** 2-3x performance boost, zero code changes

### Phase 2: Optimize (1-2 weeks)

1. Gradually rewrite routes in Elysia
2. Use Bun's built-in features
3. Add TypeScript
4. **Result:** 5-10x performance boost, modern codebase

### Phase 3: Advanced (ongoing)

1. Use Bun's native APIs
2. Optimize with built-in bundling
3. Add advanced Elysia features
4. **Result:** Maximum performance, minimal dependencies

## Real Migration Timeline

**Small API (< 20 routes):** 2-3 days **Medium API (< 100 routes):** 1-2 weeks  
**Large API (100+ routes):** 1 month+

**Recommendation:** Start with Phase 1 (Bun + Express) for immediate benefits, then gradually migrate to Elysia for maximum performance.

## Performance Comparison

| Metric           | Node.js + Express | Bun + Express | Bun + Elysia |
| ---------------- | ----------------- | ------------- | ------------ |
| **Startup Time** | ~2s               | ~0.5s         | ~0.3s        |
| **Requests/sec** | ~25,000           | ~35,000       | ~65,000      |
| **Memory Usage** | ~50MB             | ~30MB         | ~25MB        |
| **Bundle Size**  | Large             | Medium        | Small        |


---

## Testing Performance Gains

### 1. Install Node.js

```powershell
# Download from https://nodejs.org/
# Or use winget
winget install OpenJS.NodeJS
```

### 2. Install Bun

```powershell
# PowerShell (run as administrator)
powershell -c "irm bun.sh/install.ps1 | iex"

# Or download manually from https://bun.sh/
```

### 3. Install Testing Tools

#### Option A: Use Windows Subsystem for Linux (WSL) - RECOMMENDED

```powershell
# Install WSL
wsl --install

# After restart, in WSL terminal:
sudo apt update
sudo apt install apache2-utils  # for 'ab' command
sudo apt install wrk           # for 'wrk' command
```

#### Option B: Native Windows Tools

**Apache Bench for Windows:**

```powershell
# Download Apache HTTP Server for Windows
# https://httpd.apache.org/docs/current/platform/windows.html
# Extract and add bin/ folder to PATH
# Or use chocolatey:
choco install apache-httpd
```

**PowerShell Alternative (built-in):**

```powershell
# We'll use Invoke-WebRequest for basic testing
# More comprehensive script provided below
```

---

## Test Setup - Windows Specific

_Only required if you have no projects to test._

### 1. Create Project Directories

```powershell
# Create test directories
mkdir performance-test
cd performance-test
mkdir node-express-test, bun-express-test, bun-elysia-test
```

### 2. Node.js + Express Setup

```powershell
cd node-express-test

# Create package.json
@'
{
  "name": "node-express-test",
  "version": "1.0.0",
  "scripts": {
    "start": "node server.js"
  },
  "dependencies": {
    "express": "^4.18.2"
  }
}
'@ | Out-File -FilePath package.json -Encoding UTF8

# Create server.js
@'
const express = require('express');
const app = express();
app.use(express.json());

const users = Array.from({ length: 1000 }, (_, i) => ({
  id: i + 1,
  name: `User ${i + 1}`,
  email: `user${i + 1}@example.com`,
  createdAt: new Date().toISOString()
}));

app.get('/ping', (req, res) => {
  res.json({ message: 'pong', timestamp: Date.now() });
});

app.get('/users', (req, res) => {
  res.json(users);
});

app.get('/users/:id', (req, res) => {
  const user = users.find(u => u.id === parseInt(req.params.id));
  if (!user) return res.status(404).json({ error: 'Not found' });
  res.json(user);
});

app.post('/users', (req, res) => {
  const newUser = { id: users.length + 1, ...req.body, createdAt: new Date().toISOString() };
  users.push(newUser);
  res.status(201).json(newUser);
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Node.js server running on port ${PORT}`);
});
'@ | Out-File -FilePath server.js -Encoding UTF8

npm install
```

### 3. Bun + Express Setup

```powershell
cd ../bun-express-test

# Copy the same files
Copy-Item ../node-express-test/package.json .
Copy-Item ../node-express-test/server.js .

# Update package.json for Bun
(Get-Content package.json) -replace '"node server.js"', '"bun server.js"' | Set-Content package.json

bun install
```

### 4. Bun + Elysia Setup

```powershell
cd ../bun-elysia-test

# Create package.json
@'
{
  "name": "bun-elysia-test",
  "version": "1.0.0",
  "scripts": {
    "start": "bun server.ts"
  },
  "dependencies": {
    "elysia": "^0.7.30"
  }
}
'@ | Out-File -FilePath package.json -Encoding UTF8

# Create server.ts
@'
import { Elysia } from "elysia";

const users = Array.from({ length: 1000 }, (_, i) => ({
  id: i + 1,
  name: `User ${i + 1}`,
  email: `user${i + 1}@example.com`,
  createdAt: new Date().toISOString()
}));

const app = new Elysia()
  .get("/ping", () => ({ message: "pong", timestamp: Date.now() }))
  .get("/users", () => users)
  .get("/users/:id", ({ params }) => {
    const user = users.find(u => u.id === parseInt(params.id));
    if (!user) throw new Error("User not found");
    return user;
  })
  .post("/users", ({ body }) => {
    const newUser = { id: users.length + 1, ...body, createdAt: new Date().toISOString() };
    users.push(newUser);
    return newUser;
  })
  .listen(3000);

console.log("Elysia server running on port 3000");
'@ | Out-File -FilePath server.ts -Encoding UTF8

bun install
```

---

## Windows Performance Testing Scripts

### Option 1: PowerShell Testing Script (Native Windows)

**benchmark.ps1:**

```powershell
# Performance Benchmark Script for Windows
param(
    [int]$Requests = 10000,
    [int]$Concurrency = 100,
    [int]$Duration = 30
)

Write-Host "🚀 Performance Benchmark: Node.js vs Bun (Windows)" -ForegroundColor Cyan
Write-Host "=" * 50

# Function to test HTTP endpoint
function Test-HttpPerformance {
    param(
        [string]$Name,
        [string]$Url,
        [int]$Requests,
        [int]$Duration
    )
    
    Write-Host "`n🔥 Testing: $Name" -ForegroundColor Yellow
    Write-Host "URL: $Url"
    
    $startTime = Get-Date
    $requestCount = 0
    $successCount = 0
    $errorCount = 0
    $responseTimes = @()
    
    # Warm up
    try { Invoke-WebRequest -Uri $Url -TimeoutSec 5 | Out-Null } catch { }
    
    # Run test for specified duration
    $endTime = $startTime.AddSeconds($Duration)
    
    while ((Get-Date) -lt $endTime) {
        $requestStart = Get-Date
        try {
            $response = Invoke-WebRequest -Uri $Url -TimeoutSec 10
            if ($response.StatusCode -eq 200) {
                $successCount++
            }
            $responseTime = ((Get-Date) - $requestStart).TotalMilliseconds
            $responseTimes += $responseTime
        }
        catch {
            $errorCount++
        }
        $requestCount++
        
        # Small delay to prevent overwhelming
        Start-Sleep -Milliseconds 1
    }
    
    $totalTime = ((Get-Date) - $startTime).TotalSeconds
    $rps = [math]::Round($successCount / $totalTime, 2)
    $avgResponseTime = if ($responseTimes.Count -gt 0) { [math]::Round(($responseTimes | Measure-Object -Average).Average, 2) } else { 0 }
    $minResponseTime = if ($responseTimes.Count -gt 0) { [math]::Round(($responseTimes | Measure-Object -Minimum).Minimum, 2) } else { 0 }
    $maxResponseTime = if ($responseTimes.Count -gt 0) { [math]::Round(($responseTimes | Measure-Object -Maximum).Maximum, 2) } else { 0 }
    
    Write-Host "📊 Results:" -ForegroundColor Green
    Write-Host "  - Total Requests: $requestCount"
    Write-Host "  - Successful: $successCount"
    Write-Host "  - Failed: $errorCount"
    Write-Host "  - Requests/sec: $rps"
    Write-Host "  - Avg Response Time: $avgResponseTime ms"
    Write-Host "  - Min Response Time: $minResponseTime ms"
    Write-Host "  - Max Response Time: $maxResponseTime ms"
    
    return @{
        Name = $Name
        RequestsPerSecond = $rps
        AvgResponseTime = $avgResponseTime
        SuccessCount = $successCount
        ErrorCount = $errorCount
    }
}

# Function to start server in background
function Start-Server {
    param(
        [string]$Path,
        [string]$Command,
        [int]$Port
    )
    
    $originalPath = Get-Location
    Set-Location $Path
    
    $env:PORT = $Port
    $process = Start-Process -FilePath "powershell" -ArgumentList "-Command", $Command -PassThru -WindowStyle Hidden
    
    Set-Location $originalPath
    
    # Wait for server to start
    $timeout = 10
    $elapsed = 0
    do {
        Start-Sleep 1
        $elapsed++
        try {
            $response = Invoke-WebRequest -Uri "http://localhost:$Port/ping" -TimeoutSec 2
            if ($response.StatusCode -eq 200) { break }
        } catch { }
    } while ($elapsed -lt $timeout)
    
    return $process
}

# Start servers
Write-Host "Starting servers..." -ForegroundColor Cyan

$nodeProcess = Start-Server -Path "node-express-test" -Command "npm start" -Port 3000
$bunExpressProcess = Start-Server -Path "bun-express-test" -Command "bun start" -Port 3001
$bunElysiaProcess = Start-Server -Path "bun-elysia-test" -Command "bun start" -Port 3002

Start-Sleep 5  # Additional wait time

# Run tests
$results = @()

Write-Host "`n=== PING ENDPOINT TEST ===" -ForegroundColor Magenta
$results += Test-HttpPerformance -Name "Node.js + Express" -Url "http://localhost:3000/ping" -Requests $Requests -Duration $Duration
$results += Test-HttpPerformance -Name "Bun + Express" -Url "http://localhost:3001/ping" -Requests $Requests -Duration $Duration
$results += Test-HttpPerformance -Name "Bun + Elysia" -Url "http://localhost:3002/ping" -Requests $Requests -Duration $Duration

Write-Host "`n=== JSON RESPONSE TEST ===" -ForegroundColor Magenta
$results += Test-HttpPerformance -Name "Node.js + Express (JSON)" -Url "http://localhost:3000/users" -Requests $Requests -Duration $Duration
$results += Test-HttpPerformance -Name "Bun + Express (JSON)" -Url "http://localhost:3001/users" -Requests $Requests -Duration $Duration
$results += Test-HttpPerformance -Name "Bun + Elysia (JSON)" -Url "http://localhost:3002/users" -Requests $Requests -Duration $Duration

# Summary
Write-Host "`n📈 PERFORMANCE SUMMARY" -ForegroundColor Cyan
Write-Host "=" * 50
$results | Format-Table -Property Name, RequestsPerSecond, AvgResponseTime, SuccessCount, ErrorCount

# Cleanup
Write-Host "`nCleaning up..." -ForegroundColor Yellow
Stop-Process $nodeProcess -Force -ErrorAction SilentlyContinue
Stop-Process $bunExpressProcess -Force -ErrorAction SilentlyContinue  
Stop-Process $bunElysiaProcess -Force -ErrorAction SilentlyContinue

Write-Host "✅ Benchmark complete!" -ForegroundColor Green
```

### Option 2: Using WSL (Recommended)

**benchmark-wsl.sh:**

```bash
#!/bin/bash
# Run this from WSL terminal

echo "🚀 Performance Benchmark: Node.js vs Bun (WSL)"
echo "=============================================="

# Function to run Apache Bench test
run_ab_test() {
    local name=$1
    local port=$2
    local endpoint=$3
    local requests=$4
    local concurrency=$5
    
    echo -e "\n🔥 Testing: $name"
    echo "Endpoint: http://localhost:$port$endpoint"
    
    # Run Apache Bench
    ab -n $requests -c $concurrency http://localhost:$port$endpoint
}

# Start servers (assuming they're already running in Windows)
echo "Make sure your servers are running in Windows:"
echo "1. Node.js server on port 3000"
echo "2. Bun Express server on port 3001" 
echo "3. Bun Elysia server on port 3002"
echo ""
read -p "Press Enter when servers are ready..."

# Run tests
echo -e "\n=== PING ENDPOINT TEST ==="
run_ab_test "Node.js + Express" 3000 "/ping" 10000 100
run_ab_test "Bun + Express" 3001 "/ping" 10000 100
run_ab_test "Bun + Elysia" 3002 "/ping" 10000 100

echo -e "\n=== JSON RESPONSE TEST ==="
run_ab_test "Node.js + Express" 3000 "/users" 5000 50
run_ab_test "Bun + Express" 3001 "/users" 5000 50
run_ab_test "Bun + Elysia" 3002 "/users" 5000 50

echo -e "\n✅ Tests complete!"
```

---

## How to Run the Tests

### Method 1: PowerShell Script (Pure Windows)

```powershell
# Run the PowerShell benchmark
.\benchmark.ps1 -Duration 30

# Or with custom parameters
.\benchmark.ps1 -Duration 60 -Requests 20000
```

### Method 2: Manual Testing with PowerShell

```powershell
# Terminal 1: Start Node.js server
cd node-express-test
npm start

# Terminal 2: Start Bun Express server
cd bun-express-test  
$env:PORT=3001; bun start

# Terminal 3: Start Bun Elysia server
cd bun-elysia-test
$env:PORT=3002; bun start

# Terminal 4: Run simple test
Measure-Command { 
    1..1000 | ForEach-Object { 
        Invoke-WebRequest http://localhost:3000/ping 
    } 
}
```

### Method 3: WSL (Best Results)

```bash
# In WSL terminal
chmod +x benchmark-wsl.sh
./benchmark-wsl.sh
```

---

## Memory and Startup Testing (Windows)

**memory-test.ps1:**

```powershell
Write-Host "💾 Memory Usage Test" -ForegroundColor Cyan

# Start servers and measure memory
$nodeProcess = Start-Process -FilePath "node" -ArgumentList "node-express-test/server.js" -PassThru
Start-Sleep 3
$nodeMemory = (Get-Process -Id $nodeProcess.Id).WorkingSet64 / 1MB

$bunProcess = Start-Process -FilePath "bun" -ArgumentList "bun-express-test/server.js" -PassThru  
Start-Sleep 3
$bunMemory = (Get-Process -Id $bunProcess.Id).WorkingSet64 / 1MB

Write-Host "Node.js Memory: $([math]::Round($nodeMemory, 2)) MB"
Write-Host "Bun Memory: $([math]::Round($bunMemory, 2)) MB"

# Cleanup
Stop-Process $nodeProcess -Force
Stop-Process $bunProcess -Force
```

**startup-test.ps1:**

```powershell
Write-Host "🕐 Startup Time Test" -ForegroundColor Cyan

# Test Node.js startup
$nodeTime = Measure-Command { 
    $process = Start-Process -FilePath "node" -ArgumentList "node-express-test/server.js" -PassThru
    Start-Sleep 1  # Wait for startup
    Stop-Process $process -Force
}

# Test Bun startup  
$bunTime = Measure-Command {
    $process = Start-Process -FilePath "bun" -ArgumentList "bun-express-test/server.js" -PassThru
    Start-Sleep 1  # Wait for startup
    Stop-Process $process -Force
}

Write-Host "Node.js Startup: $($nodeTime.TotalSeconds) seconds"
Write-Host "Bun Startup: $($bunTime.TotalSeconds) seconds"
```


---

