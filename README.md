# Sales Management Subsystem

## Overview
The Sales Management Subsystem is a modular, enterprise-grade Java application designed to orchestrate complex sales workflows. It handles the complete lifecycle of sales operations, including customer management, lead tracking, deal progression, and quote generation.

## System Architecture
This project is engineered with a strong emphasis on clean code and scalable system design, utilizing several core Object-Oriented Design (OOD) patterns:
* **Command Pattern:** Encapsulates business logic for actions like `CreateDealCommand` and `GenerateReportCommand`.
* **Facade Pattern:** Simplifies client interactions through dedicated facades.
* **Builder Pattern:** Streamlines the instantiation of complex objects like `Customer` and `Quote`.
* **DAO (Data Access Object) Pattern:** Abstracts and secures database operations across all core entities.

## Subsystem Integrations
To function within a larger enterprise ecosystem, this module is fully integrated with two external subsystems:
1.  **Business Intelligence (BI) Subsystem:** Utilizes the `BISalesIntegrationServiceImpl` to actively publish confirmed sales records and revenue data directly into the BI database. This real-time streaming allows downstream analytics engines to visualize sales performance and generate forecasts.
2.  **Order Processing / ERP Subsystem:** Exposes a dedicated `SdkSalesQuoteGateway` that allows the external Order Processing module to securely fetch finalized `QuoteDetails` (including customer IDs and final order values) to initiate the fulfillment phase without exposing internal system logic.

## Tech Stack
* **Language:** Java
* **Database:** SQL with `HikariCP` for high-performance connection pooling and `ErpDatabaseFacade`.
* **Logging:** SLF4J for standardized application logging.

## Execution & Running the Project
The project relies on specific external JAR libraries (MySQL connector, HikariCP, SLF4J, and a local DB module). 

**Option 1: Using the build script (Recommended for Windows)**
1. Ensure your database configuration is correct in `database.properties`.
2. Open PowerShell in the project directory.
3. Run the automated build and execution script:
   ```powershell
   .\build-and-run.ps1
   This script automatically creates a bin directory, loads all necessary .jar files into the classpath, compiles the Java files, and launches the system.
   ```
**Option 2: Manual Execution**
If you are running manually, ensure you include the required dependencies in your classpath:
  ```powershell
  javac -cp ".;mysql-connector-j-9.3.0.jar;HikariCP-5.1.0.jar;slf4j-api-2.0.17.jar;slf4j-simple-2.0.17.jar;local-database-module-1.0.0.jar" -d bin *.java
  java -cp ".;bin;mysql-connector-j-9.3.0.jar;HikariCP-5.1.0.jar;slf4j-api-2.0.17.jar;slf4j-simple-2.0.17.jar;local-database-module-1.0.0.jar" SalesManagementSystem
  ```
