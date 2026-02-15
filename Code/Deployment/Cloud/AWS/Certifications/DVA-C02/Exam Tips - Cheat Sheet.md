# 📝 AWS Exam Patterns Cheat Sheet

---

## 1️⃣ Resource Explosion vs Event Routing Pattern

**Step 1 — Growth signals:**

- multiple partners / tenants
    
- future onboarding
    
- dynamic consumers
    
- unknown growth
    
- minimal code changes
    
- loosely coupled / serverless / event-driven
    

**Step 2 — Categorize answers:**

### 🚨 Resource Explosion (distractor)

- Topic per partner
    
- Queue per partner
    
- Lambda per partner
    
- API per partner
    
- DynamoDB table per tenant
    
- Step Function per customer
    

**Characteristics:**

- Publisher logic grows
    
- Deployment complexity increases
    
- Operational surface area increases
    
- Tight coupling
    

### 🏆 Event Routing / Shared Infrastructure (usually correct)

- Single event stream
    
- Shared compute
    
- Configuration-based routing
    
- Examples: SNS filters, EventBridge rules, SQS with attributes, single Lambda + tenant context, DynamoDB single-table design
    

**Step 3 — 10-second test**

1. Does infrastructure grow per tenant? → ❌ distractor
    
2. Does publisher code need updating for new consumers? → ❌ distractor
    
3. Is routing done via configuration instead of code? → ✅ correct
    

**Exam bias:** AWS prefers shared services, event-driven, fan-out, declarative routing, stateless compute.

---

## 2️⃣ Stateless Compute vs Stateful Coupling Pattern

**Step 1 — Signals:**

- Lambda / EC2 / containers
    
- Per-tenant or session state
    
- “Processing events” or “high availability”
    

### 🚨 Stateful / per-instance logic (distractor)

- Lambda writing temp files locally
    
- EC2 with local storage per tenant
    
- Single container holding session info
    

**🏆 Stateless / decoupled (usually correct)**

- Lambda + external storage (S3, DynamoDB, RDS)
    
- Containers behind load balancers with shared storage
    
- Step Functions maintaining state
    

**10-second check:**

- Can this scale horizontally without code changes? ✅
    
- Does it rely on local state? ❌
    

---

## 3️⃣ Synchronous vs Asynchronous Integration Pattern

**Step 1 — Signals:**

- API Gateway + Lambda
    
- Multiple downstream services
    
- High throughput / unpredictable traffic
    
- Need for retries, durability, or decoupling
    

### 🚨 Synchronous / tightly coupled (distractor)

- Lambda calling partner APIs directly
    
- Services waiting for responses
    
- Hard-coded retry logic
    

### 🏆 Asynchronous / decoupled (usually correct)

- SNS, SQS, EventBridge, Kinesis
    
- Lambda publishes events and moves on
    
- Consumers handle messages independently
    

**10-second check:**

- Are consumers decoupled from producer? ✅
    
- Does producer wait for responses? ❌
    

---

## 4️⃣ Single-Table / Multi-Tenant DynamoDB Pattern

**Step 1 — Signals:**

- Multiple tenants / customers
    
- Different entity types
    
- Future growth, high scalability
    

### 🚨 Multiple tables per entity / tenant (distractor)

- DynamoDB table per tenant
    
- RDS per customer
    
- Many physical resources per tenant
    

### 🏆 Single-table / shared storage (usually correct)

- Single DynamoDB table with PK/SK design
    
- Attribute-based tenant access
    
- Easier indexing and queries
    

**10-second check:**

- New tenant requires new resources? ❌
    
- Can schema handle growth via config only? ✅
    

---

## 5️⃣ Fan-Out / Fan-In Pattern

**Step 1 — Signals:**

- Events published to multiple consumers
    
- Notifications, reporting, downstream processing
    
- Scaling / high throughput
    

### 🚨 Direct calls / per-consumer logic (distractor)

- Lambda calling multiple services sequentially
    
- Hard-coded per-service logic
    
- Adding consumers requires code changes
    

### 🏆 Fan-out architecture (usually correct)

- SNS / SQS / EventBridge routing
    
- Lambda publishes once, multiple subscribers
    
- New consumers subscribe without touching publisher
    

**10-second check:**

- Adding new consumer requires code? ❌
    
- Single publisher scales without changes? ✅
    

---

## ✅ Quick AWS Exam Bias Summary

|Principle|Preference|
|---|---|
|Shared services|High|
|Event-driven / fan-out|High|
|Declarative routing|High|
|Stateless compute|High|
|Resource-per-tenant|Low|
|Duplicate Lambda logic|Very low|
|Tight coupling|Very low|

---

This cheat sheet alone covers **70–80% of the tricky serverless / messaging / multi-tenant / compute questions** on the AWS exams.


