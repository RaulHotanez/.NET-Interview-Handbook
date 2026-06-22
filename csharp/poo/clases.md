## ¿Qué es una clase?

Una clase es un tipo de referencia que define un plano técnico para los objetos. Al crear una variable de un tipo de clase, la variable contiene una referencia a un objeto en el montón administrado. La variable no contiene los datos del objeto. Asignar una variable de clase a otra variable copia la referencia, por lo que ambas variables apuntan al mismo objeto. Las clases son la manera más común de definir tipos personalizados en C#. Úselos cuando necesite un comportamiento complejo, herencia o identidad compartida entre referencias.

```csharp title="C#"
public class Customer
{
    public string Name { get; set; }

    public Customer(string name) => Name = name;
}
```


## Tipos de clases

### Clase concreta
Clases Concretas (Normales): Son el tipo más común. Permiten instanciar objetos directamente mediante la palabra clave new y contienen una implementación completa de sus propiedades y métodos.
```csharp title="C#"
public class Animal
{
    public void Speak()
    {
        Console.WriteLine("The animal makes a sound.");
    }
}

// Define a derived class that inherits from the Animal class
public class Dog : Animal
{
    public void Bark()
    {
        Console.WriteLine("The dog barks.");
    }
}
```
### Clase abstracta
Es una clase que no se puede instanciar directamente. Sirve como base para otras clases.
Puede tener métodos normales y métodos abstractos (sin implementación) que las clases hijas están obligadas a implementar.
```csharp title="C#"
public abstract class AbstractClass
{
    public abstract void abstracyMethod(); // Método abstracto

    public void MyConcreteMethod() // Método concreto
    {
        Console.WriteLine("this is a messaeg");
    }
}
```

### Clase parcial (partial)
Permite dividir una misma clase en varios archivos.
El compilador las une en una sola clase al final.
Se usa mucho cuando parte del código es generado automáticamente (por ejemplo, en WinForms o EF).
```csharp title="C#"
    public partial class User
    {
        public string Name { get; set; }
        public int Age { get; set; }
    }
```

### Clase sellada (sealed)
Es una clase que no se puede heredar.
Nadie puede crear una clase hija a partir de ella.
Se usa cuando quieres evitar extensiones o modificaciones por herencia.
```csharp title="C#"
 public sealed class Autenticacion
{
    public bool ValidarUsuario(string username, string password)
    {
        // En este ejemplo, la clase Autenticacion es sellada, lo que significa que nadie puede heredar de ella y modificar la lógica de validación.
        return (username == "admin" && password == "1234");
    }
}
```

### Clase estática (static)
Es una clase que no se puede instanciar y solo puede contener miembros estáticos.
Se usa para utilidades o funciones globales (ej: métodos matemáticos, helpers).
```csharp title="C#"
// Define a static class
    public static class MathUtils
    {
        // Static method to add two numbers
        public static int Add(int a, int b)
        {
            return a + b;
        }

        // Static method to subtract two numbers
        public static int Subtract(int a, int b)
        {
            return a - b;
        }

       // Static method to multiply two numbers
        public static int Multiply(int a, int b)
        {
            return a * b;
        }
    }
```     



## Comparación

| Tipo | Se puede instanciar | Herencia | Uso |
|-------|---------------------|----------|-----|
| Clase | ✔ | ✔ | General |
| Abstract | ❌ | ✔ | Base |
| Static | ❌ | ❌ | Utilidades |
| Sealed | ✔ | ❌ | Evitar herencia |
| Partial | ✔ | ✔ | Separar código |
| Record | ✔ | ✔ | Datos inmutables |
| Generic | ✔ | ✔ | Reutilización |

> ⚠️ **Nota importante:** falta agregar Record y Generic
