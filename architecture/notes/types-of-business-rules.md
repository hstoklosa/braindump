# Types of Business Rules

**Application-specific:** it can't be used in another application.

**Application-independent:** apply to many applications in the same domain.

**For example:**

Imagine an _order entry_ system and _order processing_ systems.

The use case _CreateOrder_ only applies to the _order entry system_ (specific).

The algorithm for _computing the price of the order_ goes _in both applications_ (independent).

Application-specific -> Service
Application-independent -> Entity

In this case, entity is a pure element of the domain model, knowing nothing about the application, but everything about the domain instead.

(Interactor/services)'s job to control the dense of the entities i.e., tells the entities what to do.

### Reference:

- [OOP 2015 Keynote - Robert C. Martin ("Uncle Bob"): Agility and Architecture](https://www.youtube.com/watch?v=0oGpWmS0aYQ)
