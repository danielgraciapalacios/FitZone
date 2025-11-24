# FitZone - Client Management System

A console-based client management system for fitness zone memberships built with Java and MySQL.

## 📋 Overview

FitZone enables comprehensive CRUD (Create, Read, Update, Delete) operations on client records, including:
- Listing all clients
- Searching by identifier
- Adding new clients
- Modifying existing client information
- Deleting clients

The system uses a dual-identifier approach where `idClient` serves as the database primary key with auto-increment functionality, while `membershipNumber` serves as the business identifier with unique constraint enforcement.

## 🏗️ System Architecture

FitZone follows a classic three-tier layered architecture with clear separation of concerns:

| Layer | Components | Responsibilities |
|-------|------------|------------------|
| **Presentation** | `ZonaFitApp` class | Menu display, user input handling, operation coordination |
| **Domain** | `Client` class | Business entity representation, data encapsulation |
| **Data Access** | `IClientDAO` interface, `ClientDAO` implementation | Database operations abstraction, SQL execution |
| **Persistence** | MySQL `fit_zone_db` database | Data storage, constraint enforcement |

## 🛠️ Technology Stack

| Component | Technology | Version | Purpose |
|-----------|------------|---------|---------|
| Programming Language | Java | 25 | Application development |
| Build Tool | Maven | 4.0.0 | Dependency management, build automation |
| Database | MySQL | 8.0.44 | Data persistence |
| JDBC Driver | MySQL Connector/J | 9.5.0 | Database connectivity |
| Character Encoding | UTF-8 | - | Source file and database encoding |

**Maven Coordinates**: `fit_zone:FitZone:1.0-SNAPSHOT`

## 🚀 Key Features

### CRUD Operations
FitZone provides six main operations through its console menu interface:

| Operation | Method | Description |
|-----------|--------|-------------|
| **List Clients** | `showClientsList()` | Retrieves and displays all clients ordered by `idClient` |
| **Search Client** | `searchClient()` | Searches for a client by database ID or membership number |
| **Add Client** | `addNewClient()` | Creates a new client record with duplicate prevention |
| **Modify Client** | `modifyClient()` | Updates client information identified by membership number |
| **Delete Client** | `removeClient()` | Removes a client record by either identifier type |
| **Exit** | Return flag | Terminates the application loop |

## 🗄️ Database Schema

The persistence layer consists of a single MySQL database with one primary table:

**Database**: `fit_zone_db`  
**Character Set**: `utf8mb4` with `utf8mb4_0900_ai_ci` collation  
**Engine**: InnoDB

### Primary Table: `clients`

| Column Name | Data Type | Constraints | Purpose |
|-------------|-----------|-------------|---------|
| `idClient` | INT | PRIMARY KEY, AUTO_INCREMENT | Database primary key |
| `first_name` | VARCHAR(50) | NOT NULL | Client's first name |
| `last_name1` | VARCHAR(50) | NOT NULL | Client's primary surname |
| `last_name2` | VARCHAR(50) | NULL | Client's secondary surname (optional) |
| `membership_number` | INT | UNIQUE | Business identifier for the client |
| `registration_date` | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | Automatic creation timestamp |
| `last_updated` | TIMESTAMP | ON UPDATE CURRENT_TIMESTAMP | Automatic modification timestamp |

## 🎯 Application Entry Point

The application starts through the `ZonaFitApp` class with the following initialization sequence:

1. **Main Method**: Entry point that calls `MainApp()`
2. **MainApp() Method**: Initializes the application
   - Creates `IClientDAO` instance using `ClientDAO` implementation
   - Initializes Scanner for user input
   - Enters menu loop until exit flag is set
3. **Menu Loop**: Continuously displays menu and processes user selections
4. **Error Handling**: Try-catch block wraps menu operations with console error output

## 📦 Build Configuration

The project uses Maven for build management with the following configuration:

- **Project Coordinates**:
  - Group ID: `fit_zone`
  - Artifact ID: `FitZone`
  - Version: `1.0-SNAPSHOT`

- **Compiler Settings**:
  - Source Compatibility: Java 25
  - Target Compatibility: Java 25
  - Source Encoding: UTF-8

- **Dependencies**:
  - `com.mysql:mysql-connector-j:9.5.0`

## 🎨 Design Patterns

FitZone implements several established software design patterns:

- **DAO (Data Access Object) Pattern**: Abstracts database operations through `IClientDAO` interface
- **Layered Architecture**: Clear separation between presentation, domain, and data access layers
- **Factory Pattern (Simplified)**: `SQLConnection.getConnection()` centralizes connection creation
- **Domain Model Pattern**: `Client` class represents core business concept with data encapsulation

## ⚠️ Current Limitations

| Limitation | Impact |
|------------|--------|
| Hardcoded database credentials | Security risk, deployment inflexibility |
| No connection pooling | Performance degradation under load |
| Console-only interface | Limited accessibility and usability |
| No configuration file support | Cannot change settings without recompilation |
| Limited error handling | Exceptions may not provide actionable information |
| No audit logging | Cannot track who performed operations or when |
| Timestamp fields not mapped | `registration_date` and `last_updated` unused in Java |

## 📁 Source Files

- `pom.xml` - Maven configuration and dependencies
- `src/main/java/fit_zone/presentation/ZonaFitApp.java` - Main application class
- `src/main/resources/db/fit_zone_db.sql` - Database creation script

## 🚀 Getting Started

1. **Database Setup**: Execute the SQL script to create the database and table
2. **Build**: Use Maven to compile the project: `mvn clean compile`
3. **Run**: Execute the `ZonaFitApp` class to start the application
4. **Configure**: Update database connection settings in the `SQLConnection` class

---

*For detailed architecture patterns, technology specifications, and component interactions, refer to the comprehensive documentation in the source code.*
