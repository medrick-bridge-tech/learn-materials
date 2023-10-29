# L : Liskov Substitution Principle

Liskov Substitution Principle was introduced by Barbara Liskov in 1987.
A derived class must be correctly substitutable for its base class.
When you derived a class from a base class then the derived class should
correctly implement all the methods of the base class.
It should not remove some methods by throwing (NotImplementedException).
LSP states that the child class should be perfectly substitutable for their parent class.
If class C is derived from P then C should be substitutable for P.

Let’s consider the code below where LSP is violated.
We cannot simply substitute a Triangle, which results in printing shape of a triangle, with Circle.

''' 
public class Program
{
   static void Main(string[] args)
   {
     Triangle triangle = new Circle();
     Console.WriteLine(triangle.GetColor());
   }
 }
 
public class Triangle
{
   public virtual string GetShape()
   {
     return "Triangle";
   }
}
 
public class Circle: Triangle
{
   public override string GetShape()
   {
     return "Circle";
   }
}

To correct above implementation, we need to refactor this code by introducing interface with method called GetShape.

'''
class Program
{
   static void Main(string[] args)
   {
     Shape shape = new Circle();
     Console.WriteLine(shape.GetShape());
     shape = new Triangle ();
     Console.WriteLine(shape.GetShape());
   }
}
 
public abstract class Shape
{
   public abstract string GetShape();
}
 
public class Triangle: Shape
{
   public override string GetShape()
   {
     return "Triangle";
   }
}
 
public class Circle: Triangle
{
   public override string GetShape()
   {
     return "Circle";
   }
}
