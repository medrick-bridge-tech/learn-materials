# Open / Closed Principle

The Open / Closed Principle, states that classes should be open for extension but closed for modification. 
This principle aims to enable the addition of new features without changing existing code, 
minimizing the risk of breaking established functionality.

## Key Concepts

- **Open for Extension**: A class should allow for extension, through creation of subclasses that can add new methods or fields.

- **Closed for Modification**: Once a class is finalized, its code should remain unchanged.
  Some programming languages use keywords like `final` to enforce this.

## Implementation

- A class can be both open (for extension) and closed (for modification) at the same time.

- When dealing with a well-established class, direct modification is discouraged to prevent potential risks.
  Instead, create a subclass, override specific parts, and introduce changes without affecting existing code.

## Considerations

- **Bug Fixes**: The Open/Closed Principle is not intended for fixing bugs. If there's a known issue, direct modification is acceptable.

- **Responsibility of Subclasses**: Child classes should focus on extending functionality rather than fixing issues in the parent class.

## Example Usage
This class has an abstract method to calculate the area of the shape:

```
public abstract class Shape
{
    public abstract double CalculateArea();
}
```

To calculate the area of a shape like circle we can create a new subclass and extend the functionality of the shape class.
We can override the abstract method to calculate the area of a circle.

```
public class Circle : Shape
{
    private double radius;

    public override double CalculateArea()
    {
        return Math.PI * Math.Pow(radius, 2);
    }
}
```
