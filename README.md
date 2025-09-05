# 🧠 Conceptos básicos en Java (para quien sabe Python)

## 📦 Clase (`class`)

Una **clase** en Java es como una **clase en Python**: es una plantilla para crear objetos.

```java
public class Persona {
    // Atributos (variables de instancia)
    String nombre;
    int edad;

    // Método (función dentro de una clase)
    public void saludar() {
        System.out.println("Hola, mi nombre es " + nombre);
    }
}
```

🟡 En Python sería:

```python
class Persona:
    def __init__(self, nombre, edad):
        self.nombre = nombre
        self.edad = edad

    def saludar(self):
        print(f"Hola, mi nombre es {self.nombre}")
```

---

## 🔁 Método (`method`)

Un **método** en Java es como una **función dentro de una clase**, similar a los métodos en Python.

```java
public void saludar() {
    System.out.println("Hola");
}
```

📌 Los métodos pueden tener un tipo de retorno (como `int`, `void`, `String`, etc.) y pueden recibir parámetros.

---

## 🧮 Variable

Una **variable** en Java es una forma de almacenar datos. Puede estar dentro de una clase, de un método, o como parámetro.

```java
int edad = 25;       // Variable local dentro de un método
String nombre = "Ana";
```

🔵 Las variables tienen **tipo**: `int`, `String`, `double`, `boolean`, etc.

---

## 🔐 Variable de instancia

Una **variable de instancia** (también llamada **atributo**) es una variable que pertenece a un **objeto**. Se define dentro de una clase, pero fuera de los métodos.

```java
public class Persona {
    String nombre;   // Variable de instancia
    int edad;        // Variable de instancia
}
```

📌 Equivale a `self.nombre` o `self.edad` en Python.

---

## 🎯 Parámetro

Un **parámetro** en Java es una variable que se pasa a un método o constructor.

```java
public void saludarConNombre(String nombre) {
    System.out.println("Hola " + nombre);
}
```

🟢 En Python sería:

```python
def saludar_con_nombre(nombre):
    print(f"Hola {nombre}")
```

---

# ✅ Resumen rápido

| Concepto en Java         | ¿Qué es?                                              | Equivalente en Python |
|--------------------------|-------------------------------------------------------|------------------------|
| `class`                  | Plantilla para objetos                                | `class`               |
| Método (`method`)        | Función dentro de una clase                           | Método                |
| Variable                 | Almacena datos (con tipo)                             | Variable              |
| Variable de instancia    | Variable propia del objeto (`this.variable`)          | `self.variable`       |
| Parámetro                | Dato que se pasa a un método o constructor            | Parámetro             |
