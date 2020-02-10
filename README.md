# SpringBootRunners

-> A Runner is an auto-executable component which is called by container on application startup only once.
-> In simple this concept is used to execute any logic (code) one time when application is started.
Types of Runners (2):
1.CommandLineRunner :- This is legacy runner (old one) which is provided in Spring boot 1.0 version.
=>It has only one abstract method “run (String… args): void”.
=>It is a Functional Interface (having only one abstract method).
=>Add one StereoType Annotation over Implementation class level (Ex:- @Component). So that container can detect the class and create object to it.


Code Setup: 
#Setup: JDK 1.8 and Eclipse / STS.
#1. Create Maven Project (simple one):-
->File    ->new    ->Maven Project (***Click check box [ v ])
-> Create Simple Project -> Next Enter Details (example)
Group Id: com.app
ArtifactId: SpringBootRunners
Version: 1.0
->Finish

#2. Open pom.xml and add parent, Properties, dependencies with plugins: -
Add details in pom.xml (Project Object Model). This file should contain bellow details in same order. It is Automatic Created with project.
      1.Parent Project Details.
      2.Properties (with java version).
      3.Dependencies (jar file details).
      4.Build Plugin.

pom.xml: -
<project xmlns="http://maven.apache.org/POM/4.0.0"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<groupId>com.app</groupId>
	<artifactId>SpringBootRunner</artifactId>
	<version>1.0</version>
           <!-- a. Parent Project details -->
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.1.2.RELEASE</version>
	</parent>
	<!--b. Versions/properties -->
	<properties>
		<java.version>1.8</java.version>
	</properties>
<!-- c. dependencies/jars -->
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter</artifactId>
		</dependency>
	</dependencies>
<!-- d. build plugins -->
	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>
</project>
#3 Create Properties file under src/main/resources folder: -
->Right click on “src/main/resources”new otherSearch and choose “File”   ->next->Enter name Ex:- application.properties -> Finish

#4 Write Spring Boot starter class under src/main/java folder: -
->Right click on “src/main/java”new  class  Enter details, like:
PackageName: com.app
Name: MyAppStarter  Finish
#5 Create one or more Runner classes under src/main/java folder with package “com.app”.

 Folder Structure of CommandLineRunner & ApplicationRunner with Ordered interface implementations:-
	 
Code:-
SpringBootRunner.java (Spring Boot Starter class) 
package com.venky.demo;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class SpringBottRunnerExApplication {
	public static void main(String[] args) {
		SpringApplication.run(SpringBottRunnerExApplication.class, args);
		System.out.println("Hello Venkat");
	}
}
#Runner #1: MyTestRunner1.java
package com.venky.demo.runner;
import org.springframework.boot.CommandLineRunner;
import org.springframework.core.Ordered;
import org.springframework.stereotype.Component;
@Component
/*CommandLineRunner with Ordered implementations Manual Approach*/
public class MyTestRunner implements CommandLineRunner,Ordered{
@Override
	public void run(String... args) throws Exception {
		System.out.println("-----From MyTestRunner----");
	}
	@Override
	public int getOrder() {
		return 55;
	}
}
#Runner #2: TypeARunner.java
package com.venky.demo.runner;
import org.springframework.boot.CommandLineRunner;
import org.springframework.core.annotation.Order;
import org.springframework.stereotype.Component;
@Component
@Order(53)
public class TypeARunner implements CommandLineRunner {
	@Override
	public void run(String... args) throws Exception {
		System.out.println("----From TypeARunner----");		
	}
}
Output :-
 
NOTE :-
1. Boot Application can have multiple runners 
Ex:- Email Runner, JmsRunner, SecurityRunner, CloudEnvRunner, DevOpsRunner, DatabaseRunner etc…
2. Boot provides default execution order.
->To specify programmer defined order use 
Interface: Ordered (or) Annotation: @Order 
->If we are configures both Runners but not implements Ordered then by default Annotation based Config	 uration will be executed first.


