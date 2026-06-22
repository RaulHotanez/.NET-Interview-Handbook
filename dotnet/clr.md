## CLR
________________________________________
El CLR (Common Language Runtime) es uno de los conceptos más importantes de .NET y una pregunta muy frecuente en entrevistas.
La forma más sencilla de entenderlo es esta:
El CLR es el motor de ejecución de .NET. Es el encargado de ejecutar tu código y proporcionar servicios como la administración de memoria, el Garbage Collector, el manejo de excepciones y la seguridad.

### ¿Cómo funciona?
Cuando escribes un programa en C#:
```csharp title="C#"
Console.WriteLine("Hola Mundo");
```

No se convierte directamente en código máquina.
El proceso es:
```csharp title="C#"
Código C#
      │
      ▼
Compilador C# (csc)
      │
      ▼
IL (Intermediate Language)
      │
      ▼
CLR
      │
      ▼
JIT Compiler
      │
      ▼
Código Máquina
      │
      ▼
CPU
```

