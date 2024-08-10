# Introduction
The Event Sourcing pattern stores each data change as a sequence of events in an append-only store. Instead of directly updating the data, the application records events that describe the changes. These events are the authoritative source of the current state. The store acts as the system of record and can be used to materialize the domain objects. 

# Context and Problem

Applications often manage data by updating its current state, following the CRUD (Create, Read, Update, Delete) model. This approach can slow down performance, limit scalability, and cause conflicts when multiple users work concurrently. Additionally, it can lead to a loss of history unless a separate audit log is maintained.

# Solution: Event Sourcing

Using event sourcing pattern which stores the events so that other systems can respond to them, such as updating materialized views or integrating with external systems. The pattern also decouples the code generating events from the systems that use them.

# How Event Sourcing Works

The fundamental idea of Event Sourcing is that every change to the state of an application is captured in an event object. These event objects are stored in the sequence they were applied, and they are retained for the same lifetime as the application state itself.

**Key features of Event Sourcing include:**

- **Complete Rebuild**: The application state can be discarded and completely rebuilt by re-running the events from the event log on an empty application.
  
- **Temporal Query**: The application state can be determined at any point in time by starting with a blank state and rerunning the events up to a specific time or event. This can be extended to consider multiple timelines, similar to branching in version control systems.

- **Event Replay**: If a past event was incorrect, its consequences can be computed by reversing it and later events, and then replaying the corrected event and subsequent events. This technique also handles events received in the wrong sequence, a common issue with asynchronous messaging systems.

# References

- [Microsoft Azure Architecture Patterns: Event Sourcing](https://learn.microsoft.com/en-us/azure/architecture/patterns/event-sourcing)
- [Martin Fowler: Event Sourcing](https://martinfowler.com/eaaDev/EventSourcing.html)
- [Microservices.io: Event Sourcing Pattern](https://microservices.io/patterns/data/event-sourcing.html)