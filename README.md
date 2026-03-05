**English** | [Español](README_ES.md)

# B-Ganos UML & Model-Driven Development

## Overview

This repository contains the complete **UML design and model-driven architecture** of the B-Ganos Management System.

The project was developed during the **Software Modeling course** (3rd year, Software Engineering, Universidad Complutense de Madrid, 2024–2025) by a 12-member team.

This repository does not only contain documentation artifacts, it also reflects a full **model-driven development process** in which UML models were directly transformed into executable Java code.


> The system was first fully modeled in UML and later the Java code was automatically generated from the model using IBM Rational Software Architect Designer (RSAD).

This repository therefore represents the architectural backbone from which the application was generated.

---

## Model-Driven development approach

The development workflow was:

1. Design the multilayer architecture in UML.
2. Define domain entities, services, persistence components, and presentation structure.
3. Configure the UML-to-Java transformation (`UML2JAVA.tc`).
4. Generate the initial Java project structure automatically from the model.
5. Complete and refine the implementation.

This approach ensured:

- Architectural consistency
- Clear separation of layers
- Reduced repetitive manual code
- Strong alignment between design and implementation

---

## System architecture

The UML model defines a multi-layer architecture:

- **Presentation layer**
- **Business layer**
- **Integration layer**

The system interacts with a relational database managed through the persistence mechanisms modeled in the integration layer.

Key architectural mechanisms modeled include:

- DAO pattern (SQL-based persistence)
- JPA persistence
- Transaction management
- Application Controller pattern
- Service to Worker pattern
- Business Objects and Transfer Objects separation
- Factory patterns
- Concurrency control mechanisms

---

## Persistence model

The system persistence layer was designed using **two complementary approaches**: DAO-based persistence and JPA-based persistence.

Both persistence models follow the same structural requirements.

### DAO model

The DAO persistence model is based on the **Data Access Object (DAO) pattern**, where database access is implemented manually using SQL and JDBC components. It includes:

- **6 entities**
- **2 specialized entities (inheritance)**
- **2 many-to-many relationships**
  - one with attributes in the relationship
  - one without attributes


Additionally, the DAO model includes **custom query objects** used to implement complex database queries required by the project specification.

Examples include:

- `CalculateTopThreeSalesDatesForGreenhouse`
- `ListManufacturerInformationByGreenhouseIrrigationSystems`

These queries are managed through a **Query Factory** that creates the corresponding query objects.

The six DAO entities defined in the system are:

- Invernadero (Greenhouse)
- Planta (Plant)
- Factura (Invoice)
- Fabricante (Manufacturer)
- Entrada (Entry)
- SistemaDeRiego (IrrigationSystem)

These entities are managed through DAO interfaces and implementations responsible for direct SQL interaction.

### JPA model

The JPA persistence model uses **Java Persistence API (JPA)** to manage database interaction through object-relational mapping. It includes:

- **6 JPA entities**
- **2 specialized entities (inheritance)**
- **2 many-to-many relationships**
  - one with attributes in the relationship
  - one without attributes

The JPA model also demonstrates the use of **entity inheritance and polymorphic operations**, allowing specialized entities to extend base domain entities.


The six JPA entities defined in the system are:

- ProveedorJPA (SupplierJPA)
- ProductoJPA (ProductJPA)
- TurnoJPA (ShiftJPA)
- VentaJPA (SaleJPA)
- MarcaJPA (BrandJPA)
- EmpleadoDeCajaJPA (CashierEmployeeJPA)

This model demonstrates an alternative persistence approach where database operations are managed through entity mappings instead of manual SQL.

---

## Layer modeling

The UML design organizes the system into three main layers.  
Each layer encapsulates a specific set of responsibilities and interacts with the others through clearly defined interfaces.

### Integration layer modeling

The integration layer defines the **persistence and database interaction mechanisms**.

- DAO interfaces and implementations (example: `EntradaDAO`, `EntradaDAOImp`)
- Transaction manager components
- JDBC elements (Connection, PreparedStatement, ResultSet)
- Exception handling
- Factory and query abstractions

---

### Business layer modeling

The business layer models the **core domain logic of the system** and the application use cases.

It includes:

- Domain entities representing the main business concepts
- Business services responsible for implementing operations
- Service implementations
- Transfer Objects used for communication with the presentation layer
- Business factories used to obtain service instances

Example business services include:

- `EntradaSA`
- `MarcaSA`
- `SistemaDeRiegoSA`

Supporting infrastructure components include elements such as `EMFSingleton`, responsible for managing the persistence context.

---
### Presentation layer modeling

The presentation layer models:

- ApplicationController
- Request dispatching from the controller to business services
- GUI components (Swing-based)
- Interaction with Transfer Objects (example: `TMarca`)
- Controller-to-service communication flow

---

## Main UML artifacts

The most relevant design artifacts include:

- **Class diagrams**
  - Domain entities representing the system's core business concepts
  - DAO interfaces and implementations
  - Business services
  - Presentation controllers and GUI components
- **Sequence diagrams**
  - Transactional operations
  - Use case execution flows
  - Controller → Service → DAO interactions
- **Component diagram**
  - System layer separation
  - Module dependencies
- **Deployment diagram**
  - Application deployment structure
  - Database integration
- **Entity-Relationship diagrams**
	
	Separate ER diagrams are included for:

  - DAO persistence model
  - JPA persistence model

---

## Repository structure (simplified)

```
B-Ganos-UML-Modeling/
├── Diagrams/
│ ├── Deployment Model/
│ │ ├── Component Diagrams/
│ │ └── Deployment Diagrams/
│ └── Design Model/
│ │ ├── Class Diagrams/
│ │ ├── Sequence Diagrams/
│ │ └── Free-form Diagrams/
│
├── Models/
│ ├── Deployment Model/
│ └── Design Model/
│ │ ├── Integration/
│ │ ├── Business/
│ │ └── Presentation/
│
├── Entity-Relationship Diagram/
│ ├── DAO.drawio.png
│ └── JPA.drawio.png
│
├── JPA Content/
│ └── persistence.xml
│
├── UML2JAVA.tc
└── src/ (empty - required by the Eclipse/RSAD project structure)
```

> **Note:** The original project structure in the modeling environment (IBM RSAD) is entirely in Spanish. Folder names have been translated here for documentation clarity, but the original UML model preserves the Spanish naming conventions used during development.

---

## Project documentation

The repository also contains extensive documentation produced during the project:

### Software Requirements Specification (SRS)

A **105-page requirements specification document** describing:

- System functionality
- Use cases
- Domain concepts
- System requirements
- Initial design artifacts

The document also includes **entity-relationship diagrams** for both the DAO and JPA persistence models.

### Project report

A detailed project report describing:

- System architecture
- Architectural patterns used in the system
- The modeling process
- Project management and development tools used during the project

---

## Tools used

- UML 2.x
- IBM Rational Software Architect Designer (RSAD) 9.6
- UML-to-Java transformation
- Java 8 (target environment)

---

## Code Implementation

The implementation of the system derived from this UML model is available in a separate repository. It can found here:

https://github.com/melanydece/BGanos-java-application

---

## Team

Developed collaboratively by a 12-member team as part of an advanced Software Engineering course project. The full list of contributors can be found in the repository's "Contributors" section.