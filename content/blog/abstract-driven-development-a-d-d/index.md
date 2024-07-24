---
title: Abstract Driven Development (A.D.D)
date: 2024-07-24T21:18:47
description: Abstract Driven Development (A.D.D) is a methodology that
  emphasizes the use of abstractions and layering to create scalable,
  maintainable, and flexible software systems.
---

### Overview

Abstract Driven Development (A.D.D) is a methodology that emphasizes the use of abstractions and layering to create scalable, maintainable, and flexible software systems. A.D.D aims to achieve the following goals:

- **Simplicity / KISS (Keep It Simple, Stupid)**: Ensure the methodology is easy to apply and understand, maintaining a short learning curve by avoiding an overload of new concepts.
- **Scalability**: Make it suitable for projects of all sizes, from microservices to large-scale applications.
- **Clarity**: Provide a clear classification of components into respective layers.

By maintaining these properties, systems using A.D.D can ensure extensibility, easy maintenance, and seamless replacement of system components.

Below is a detailed breakdown of its core concepts and principles.

### Key Concepts

#### Dependency Inversion

- **Base Principle**: High-level modules should not depend on low-level modules. Both should depend on abstractions.
  ![[Pasted image 20240724165056.png]]
  ![[Pasted image 20240724165215.png]]
- **Application in A.D.D**: Apply dependency inversion across different layers of the application.
![[Pasted image 20240724170426.png]]
#### Abstraction Levels

- **Abstract**: Interfaces and abstract components.
- **Concrete**: Implementations of the abstract components.

#### Components

- **Data Components**: Data Transfer Objects (DTOs), entities.
- **Action Components**: Services that perform actions on the data.

#### Coupling of the Components

- **Tightly Coupled**: Components that are difficult to replace (e.g., `EntityFramework.Core`).
- **Loosely Coupled**: Components that are easy to switch (e.g., `EntityFramework.Postgres`, `EntityFramework.Sqlite`).

### Layers

1. **Abstract Contract Layer**: Abstraction for interacting with the outside.
    - Defines external contracts and interfaces for the system.
    - Independent of any specific technology or framework.
    - Includes Data Transfer Objects (DTOs) to transport data between the outside and the Business Application, feature interfaces, and outer events (a kind of DTO).

2. **Abstract Domain Layer**: Abstraction for inner interaction.
    - Independent of any specific technology or framework.
    - Defines entities, interfaces, abstract classes, and inner events.
    - **Entities**: Only have fields and validation rules on the fields. An entity is a type of DTO used internally.
    - Listens to and processes outer events.
    - **Inner events**: Also called domain events, used internally between the Business Application & Concrete Infrastructure. Can fire and listen to inner events, which may also originate from the Infrastructure layer.

3. **Concrete Business Layer**
    - Contains core business logic. Implements application features (only what is described from the contract layer). Does not implement functions from the service interfaces in the Domain.
    - Handles outer events.
    - Handles conversion between DTOs and Entities (e.g., AutoMapper profiles can be placed in this layer).
    - Implements outputs such as Minimal APIs or controllers.

4. **Concrete Implementation Layer**
    - Provides concrete implementations of services, repositories, inner event publishers, and integrations.
    - Integrates with databases, message queues, and other infrastructure components.
    - This layer might have multiple versions (e.g., version for Postgres, version for Mongo, etc.). Initially, the system might run with a mock infrastructure layer, which does nothing and only returns default values.

5. **Program Layer**
    - This is the layer for the executable file.
    - References the Business Application Layer & Concrete Infrastructure Layer.
    - Defines dependency injection.
    - Handles other tasks for initializing the application (what is not related to the business).

### Layer Interactions / DTO Types

- **No Cross-Layer References**: Each (concrete) layer should only interact (i.e., directly call functions) with the (abstract) layers directly above or below it.
    - **Business Layer** can only see Contract and Domain Layers.
    - **Infrastructure Layer** can only see Domain Layer.
- **No direct communication between concrete layers**: The concrete layers only send out events for other concrete layers to listen to.

![[Pasted image 20240724172357.png]]

### Placing Components in Layers

The A.D.D principle ensures that at any given time, a component can be easily identified for its layer based on the following template:
- **Abstract Contract Layer**
  - DTOs
  - Outer Events
  - External service interfaces (the services in Business Layer)
- **Abstract Domain Layer**
  - Entities
  - Events
  - Internal Service Interfaces (the services in Infrastructure Layer)
- **Concrete Business Layer**
  - Services implementation
  - Event listeners (they are services too)
- **Concrete Implementation Layer**
  - Services implementation
  - Event listeners

For components that are not clearly identified for a specific layer, answer the following questions:

- Is it abstract? If yes, it goes to Contract/Domain Layer.
- Is it concrete? If yes, it goes to Business/Infrastructure Layer.
- Will there be multiple kinds of this component in the future?
  - If yes, it goes to the Infrastructure Layer.
  - If no, it goes to the Business Layer.

### Implementation Strategies

#### For Big Projects (From BRD)

1. **Define Contract Layer**
   - DTOs: Based on real-world inputs (e.g., papers, identity cards).
   - External Services: Defined by the system's main functions.
2. **Define Domain Layer**
   - Entities and internal services for the big services.
   - Events that will be used within the system.

#### For Small Projects (From Scratch)

1. **Initial Program**: Write a basic program that can run.
2. **Refactoring**: Break the code into DTOs, interfaces, and services, then move them into appropriate layers.

#### For Existing Code

1. **Reorganization**: Classify and move components into layers by asking:
   - Is it abstract? If yes, it goes to Contract/Domain Layer.
   - Is it concrete? If yes, it goes to Business/Infrastructure Layer.
   - Will there be multiple kinds of this component in the future?
     - If yes, it goes to the Infrastructure Layer.
     - If no, it goes to the Business Layer.

### Suggested Writing Order

#### For Big Projects

1. **Contract Descriptors Layer**
2. **Abstract Domain Layer**
3. **Business Application Layer**
4. **Concrete Infrastructure Layer**

#### For Small Projects

1. **Runnable Program**: Start with a monolith.
2. **Generate Unit Test**: Ensure functionality.
3. **Generate the Layers**: Refactor into layers.

### Conclusion

Abstract Driven Development provides a structured approach to software design and development, ensuring that systems are scalable, maintainable, and flexible. By following the layering and abstraction principles, developers can create robust systems that are easy to understand and evolve over time.