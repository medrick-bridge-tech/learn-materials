# Dependency Inversion Principle

## In summary:
> High-level classes should not depend on low level classes, that's easy
> 
> Both high level and low level classes should depend on abstractions
> 
> Abd details should depend on abstractions not the other way around

## What is low level and high level anyways?

### Low level:
Basic operations such as disks, databases, networks

### High level:
Contains complex business logic that directs the low level classes to do something

## Why start with low level classes
When developing a prototype, we start with the low level classes, why?

It's simple, it's a prototype, we don't know the bussiness logic yet, cause the low level is not clear.

With this approach, higher level classes will depend on low levels.

## Let's invert this
That's when dependency inversion comes to save us...

- Describe interfaces for low level classes for high level classes
  - Example: Instead of OpenFile, ReadBytes, CloseFile the high level should just call OpenReport
- Now low level classes should implement the interfaces and they become dependant of bussiness logic

## So what?
Now if there's a change in the way we read files, the high level classes do no need to change in order to adapt with the new implementation

![image](https://github.com/medrick-bridge-tech/learn-materials/assets/42384597/3e259057-f6d4-4bf6-ad4e-086a1d12b095)
