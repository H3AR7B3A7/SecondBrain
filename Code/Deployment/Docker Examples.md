# Docker Examples
## MySQL
### Creating MySQL Server container
>docker run --name MySQL -e MYSQL_ROOT_PASSWORD=pass -p 3306:3306 -d mysql:latest  
  
### Creating PgAdmin4 Container
> docker run --name phpMyAdmin -d -e PMA_HOST=MySQL --link MySQL -p 8081:80 phpmyadmin:latest  
  
The application will be running on:  
  
http://localhost:8081

## Postgres
### Creating Postgres Server container
> docker run -p 5432:5432 --name myPostgres -e POSTGRES_PASSWORD=mysecretpassword -d postgres:alpine  
  
*The default password = postgres*  
  
### Creating Postgres Server container with Docker volumes
Create a folder, for example: ‘C:/data/pg’    
> docker run -p 5432:5432 --name myPostgres -e POSTGRES_PASSWORD=mysecretpassword -v C:/data/pg:/var/lib/postgresql/data  
-d postgres:alpine  
  
### Creating PgAdmin4 Container
> docker run -p 5050:80 --name pgadmin4 -e PGADMIN_DEFAULT_EMAIL=”steven.d.hondt.sdh@gmail.com” -e PGADMIN_DEFAULT_PASSWORD=”pass” dpage/pgadmin4:latest  
  
The application will be running on:  
  
http://localhost:5050  
  
### Using either PgAdmin4 installation or container
PgAdmin4 > Servers > New Server    
Host name / address: PC-NAME / IPv4 address   
Port: 5432    
Username: postgres    
Password: pass  
  
*We can get the Host name or IPv4 address of our machine easily with following command:*  
  
- Windows  
> ipconfig /all  
  
- Linux  
> ip a

## Spring
### Maven
>mvn -N io.takari:maven:wrapper  
>mvnw spring-boot:build-image  
  
To skip tests (not recommended):   
```xml
<plugin>
	<groupId>org.apache.maven.plugins</groupId>
	<artifactId>maven-surefire-plugin</artifactId>
	<version>2.22.2</version>
	<configuration>
		<skipTests>true</skipTests>
	</configuration>
</plugin>
```
Tag and Push image to Docker HUB  
  
### Gradle
>gradlew build  
  
>docker build --build-arg JAR_FILE=build/libs/tjenterprise-0.0.1.jar -t h3ar7b3a7/tjenterprise .  
  
or with Dockerfile:  
  
 FROM openjdk:8-jdk-alpine ARG JAR_FILE=build/libs/tjenterprise-0.0.1.jar COPY ${JAR_FILE} app.jar ENTRYPOINT ["java","-jar","/app.jar"]  
Tag and Push image to Docker HUB

---
#Docker