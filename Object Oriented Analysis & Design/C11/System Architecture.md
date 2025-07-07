___
# Overview
System architecture describes how components in a software system interact, the technologies used, and how it meets the functional and non-functional requirements.
# System Architecture in Software Development
- Ensures Scalability and Performance
- Facilitates Maintainability and Flexibility
- Aligns with Business Goals
- Enhances Team Collaboration
- Mitigates Risks
# Key Concepts of System Architecture
- Layers of Architecture: provide the structural framework.
- Architectural Patterns: offer reusable solutions tailored to specific needs.
- Non-Functional Requirements: ensure the system meets performance and operational goals.
- Stakeholders and Their Roles: ensure the architecture serves its intended purpose and satisfies all involved parties.
# Layers in Architecture
- Presentation Layer: Manages user interface and user interactions.
- Business Logic Layer: Processes data and applies business rules.
- Data Access Layer (Optional): Handles database operations and external APIs.

## Microservices Vs Monolithic Architecture.

# Model-View-Controller (MVC)
![[MVC.png]]

| Aspect       | View → Model                        | View → Controller → Model                       |
| ------------ | ----------------------------------- | ----------------------------------------------- |
| Usage        | Read-only                           | Read/write, user actions                        |
| Complexity   | Simpler                             | More structured                                 |
| Coupling     | Tight (View ↔ Model)                | Loose (View → Controller ↔ Model)               |
| Testability  | Lower                               | Higher                                          |
| Suitable for | Small/simple apps, observer pattern | Larger apps, complex logic, UI-driven behaviour |
| Name         | Hard-code                           |                                                 |

- - Use **`View → Model`** for **simple data display** or when using data binding.
- Use **`View → Controller → Model`** when you need to **process input, validate data**, or enforce logic before modifying the model.