# Übung 1: Geometrische Formen

## Lösung

```csharp
using System;

namespace GeometricShapes
{
    public abstract class Shape
    {
        public string Name { get; set; }
        public abstract double CalculateArea();
        public abstract double CalculatePerimeter();
    }

    public class Circle : Shape
    {
        public double Radius { get; set; }

        public override double CalculateArea()
        {
            return Math.PI * Radius * Radius;
        }

        public override double CalculatePerimeter()
        {
            return 2 * Math.PI * Radius;
        }
    }

    public class Rectangle : Shape
    {
        public double Length { get; set; }
        public double Width { get; set; }

        public override double CalculateArea()
        {
            return Length * Width;
        }

        public override double CalculatePerimeter()
        {
            return 2 * (Length + Width);
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            Shape[] shapes = new Shape[2];
            shapes[0] = new Circle { Name = "Kreis", Radius = 5 };
            shapes[1] = new Rectangle { Name = "Rechteck", Length = 5, Width = 4 };

            foreach(var shape in shapes)
            {
                Console.WriteLine($"{shape.Name}:");
                Console.WriteLine($"- Fläche: {shape.CalculateArea():F2}");
                Console.WriteLine($"- Umfang: {shape.CalculatePerimeter():F2}\n");
            }
        }
    }
}
```
