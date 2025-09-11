# 3. Bloques básicos de clases de Java

- **Objeto:**
  - instancia de la clase en tiempo de ejecución .
  - objetos de distintas clases = estado del programa .
- **Clases:**
  - **métodos (funciones / procedimientos):** operan es ese estado + pueden ser llamadas
  - **propiedades (atributos / variables de instancia):** mantienen el estado del programa + almacenan cambios grandes
  - solo 1a clase puede ser pública por archivo. 
- **Keywords / palabras reservadas:**
  - *'public':* modificador de acceso que indica que puede ser llamado desde otra clase
  - *'void':* no devuelve nada
  - *'static':* enlaza un método a su clase para que pueda ser llamado solo por el nombre de la case, por ejemplo, *Fruit.main()* . No es necerario crear un objeto para llamar el método *main()*.
- **Parámetro:** info a dar a un método cada vez que se le llama
- **Comentarios:**
  - ```java
    // comment until end of line
  - ```java
    /* Multiple
    * line comment
    */
  - ```java
    /**
    * Javadoc multiple-line comment
    */
- **Javadoc:** (se sigue teniendo que poner dentro de un comentario)
  
| TAG         | DESCRIPCIÓN                                                                 |
|-------------|------------------------------------------------------------------------------|
| @author     | Nombre del desarrollador.                                                    |
| @deprecated | Indica que el método o clase es obsoleto (propio de versiones anteriores) y que no se recomienda su uso. |
| @param      | Definición de un parámetro de un método, es requerido para todos los parámetros del método. |
| @return     | Informa de lo que devuelve el método, no se aplica en constructores o métodos "void". |
| @see        | Asocia con otro método o clase.                                              |
| @version    | Versión del método o clase.                                                  |

- **Método *main()*:** dónde un programa Java comienza su ejecución.
- **Vocabulario:**
  - JVM (Máquina Virtual Java) : Encargada de comunicarse con el sistema subyacente para asignar recursos como la 
memoria, la CPU, el acceso a archivos, etc.
  - JRE (Java Virtual Machine) : para ejecutar el código. 
  - JDK (Java Development Kit) : para compilar Java.
  - IDE (Integrated Development Environment) : Eclipse o Netbeans para programar código Java.
  - JAR : como un archivo ZIP que únicamente contiene clases Java
- **Ejecutar:**
  ```Java
  $ javac Fruit.java
  $ java Fruit
- **Argumentos:**
  - 1er arg : *arg[0]*
  - arg con varias palabras : *"Hola Adiós"*
- **Importaciones:**
  - wildcard : importación de todas las clases de un paquete
    ``` Java
    import java.util.*;
  - en caso de tener dos clases de diferentes paquetes con el mismo nombre :
    ```Java
    import java.util.Date;
    import java.sql.Date; // no compila !

    // Solución 1 : 
    import java.util.Date;
    import java.sql.*;

    // Solución 2 :
    import java.util.*;
    import java.sql.Date;

    // Solución 3
    import java.util.Date;
    public class Conflicts {
      Date date; //Usa la clase java.util.Date
      java.sql.Date sqlDate; //Usa la clase java.sql.Date
    }

- **Ejecutar Java desde la línea de comandos:**
  - Windows :
    ```Java
    C:\temp\packagea\ClassA.java // crear el archivo
    cd C:\temp // ir a C:\temp
  - Mac OS / Linux :
    ```Java
    /tmp/packagea/ClassA.java // crear el archivo
    cd /tmp // ir a /tmp
  - Finalmente :
    ```Java
    javac packagea/ClassA.java // compila
    java packagea.ClassA // ejecuta

    // Frase 'Got it' se mostrará en la consola si todo funciona correctamente . 
- **Especificar la ubicación de otros archivos utilizando rutas:**
   - Windows :
    ```Java
    java -cp ".;C:\temp\someOtherLocation;c:\temp\myJar.jar" myPackage.MyClass
    ```
  - Mac OS / Linux :
    ```Java
    java -cp ".:/tmp/someOtherLocation:/tmp/myJar.jar" myPackage.MyClass
    ```
- **Objeto:** instancia de una clase.
  ```Java
  Random r = new Random();
  ```
  - Método constructor: encargados de crear nuevos objetos + mismo nombre que la clase + no hay return + inicializa las propiedades de un variable
    ```Java
    public class Chick {
     public Chick() {
     System.out.println("in constructor");
    }

    pubic void Chick() {} // NO es un constructor porque aunque sea 'void' estamos específicando el tipo de return y es, por tanto, un método normal
    ```
  - Leer y modificar propiedades de objetos :
    ```Java
    public class Swan {
      int numberEggs;// variable de instancia o propiedad de la clase Swan
      public static void main(String[] args) {
        Swan mother = new Swan();
        mother.numberEggs = 1; // modifica la propiedad
        System.out.println(mother.numberEggs); // lee la propiedad
      }
    }
    ```
- **Bloque de código:**  dentro de *{}* .
  - Bloque inicializador de instancia no puede estar dentro de un método.
  - Orden de inicialización :
    1. Propiedades + bloques de iniciación de instancias en orden de escritura
    2. Constructores
- **Referencias a objetos vs primitivas de datos:**
  - Primitivas de datos :
    | Palabra reservada (keyword) | Tipo                              | Ejemplo   |
    |-----------------------------|-----------------------------------|-----------|
    | boolean                     | true o false                     | True      |
    | byte                        | Valor entero de 8 bits            | 123       |
    | short                       | Valor entero de 16 bits           | 123       |
    | int                         | Valor entero de 32 bits           | 123       |
    | long                        | Valor entero de 64 bits           | 123       |
    | float                       | Valor en coma flotante de 32 bits | 123.45f   |
    | double                      | Valor en coma flotante de 64 bits | 123.456   |
    | char                        | Valor Unicode de 16 bits          | 'a'       |

    ```Java
    int max = 3123456789; //NO COMPILA , demasiado grande para ser int
    long max = 3123456789L; // Ahora es cuando Java comprende que el número es un long
    ```

    ```Java
    int million1 = 1000000; // compila
    int million2 = 1_000_000; // compila
    double notAtStart = _1000.00; //NO COMPILA
    double notAtEnd = 1000.00_; //NO COMPILA
    double notByDecimal = 1000_.00; //NO COMPILA
    double goodOne = 1_00_0.0_0; //COMPILA
    ```
  - Tipos de referencia : Un tipo referencia es un objeto (un objeto es una instancia de una clase). Al contrario que ocurre con las  primitivas de datos, que guardan sus valores directamente en la memoria reservada por la variable, los  tipos referencia no guardan los valores de los objetos en la dirección de memoria reservada cuando las  variables son declaradas. En lugar de eso, la referencia “apunta” al objeto asignado a la variable  guardando la dirección de memoria donde este se encuentra, concepto también conocido como puntero
  - Diferencias clave :
    - las variables de referencia pueden tener valor *null* (ningún objeto asignado) al contrario de las primitivas de datos.
    - los tipos referencia pueden ser utilizados para llamar métodos siempre y cuando no sean null. Las primitivas de datos no tienen métodos. (se puede saber que es un método si utiliza *()* )
    - primitivas - letra minúscula , clases - letra mayúscula .
- **Variable:** espacio de memoria donde se guardan datos.
  ```Java
  boolean b1, b2;
  String s1 = "1", s2;
  double d1, double d2; // no compila
  int i1; int i2;
  int i3; i4; // no compila

  3DPointClass // Los identificadores no pueden comenzar por un número
  hollywood@vine // @ no es una letra, dígito, $ o _
  *$coffee // * no es una letra, dígito, $ o _
  public // public es una palabra reservada
  ```
    - variable local : definida dentro de un método. Debe ser inicializada antes de su uso.
      ```Java
      public void eat(int piecesOfCheese) { //  1a variable , es un parámetro de método local al método
       int bitesOfCheese = 1; // 2nda variable , declarada dentro del método
      }
      ```
    - variable de clase (si tiene la palabra *'static'* en su declaración) e instancia ( = *'fields'*) : no requieren ser inicializadas + al alcanze durante toda la vida del programa
        - Variables de instancia: en el ámbito de aplicación de la declaración hasta que se recoge la basura del objeto (*garbage collector*).
        - Variables de clase: en el ámbito de aplicación de la declaración hasta que finalice el programa.
      
        | Tipo de variable            | Valor por defecto de inicialización          |
        |-----------------------------|----------------------------------------------|
        | boolean                     | false                                        |
        | byte, short, int, long      | 0 (en la longitud de bits del tipo)          |
        | float, double               | 0.0 (en la longitud de bits del tipo)        |
        | char                        | '\u0000' (NUL)                               |
        | Todas las referencias a objetos | Null                                     |

- **Garbage Collector (GC):**  proceso de liberar automáticamente la memoria en el heap borrando objetos que ya no son accesibles en un programa; es decir, objetos que han quedado desreferenciados
  - *heap* : gran grupo de memoria no utilizada asignada a una aplicación Java. Tiene un límite de tamaño.
  - método *' System.gc() '* : ejecuta el Garbage Collector. Puede ser ignorada y, por tanto, no siempre puede ejecutar el GC.
  - objetos vs referencias :
    - La referencia es una variable que tiene un nombre y se puede utilizar para acceder al contenido de un objeto. Se puede asignar una referencia a otra referencia, pasarla a un método o devolverla desde un método. Todas las referencias son del mismo tamaño, independientemente de su tipo.
    - Un objeto se deposita en el heap y no tiene nombre. Por lo tanto, no hay manera de acceder a un objeto  excepto a través de una referencia. Los objetos vienen en todas las formas y tamaños diferentes y consumen cantidades variables de memoria. Un objeto no se puede asignar a otro objeto, ni tampoco se puede pasar un objeto a un método o devolverlo desde un método. Es el objeto quien recibe el Garbage Collection, no su referencia
  - *'finalize()'* :
    - Es un método que puede implementar un objeto.
    - El **Garbage Collector (GC)** lo llama antes de eliminar el objeto de memoria.
    - Si el GC no se ejecuta, *'finalize()'* puede que nunca se llame.
    - Si ya se llamó una vez, no se volverá a llamar.
    ```java
    public class Finalizer {
        protected void finalize() {
            System.out.println("Adiós objeto!");
        }
        public static void main(String[] args) {
            Finalizer f = new Finalizer();
            f = null; // ahora es basura
            System.gc(); // pedimos al GC que limpie (no es seguro que lo haga)
        }
    }
    ```
    - Por qué no usarlo ? :
      - No está garantizado que se ejecute (puede que nunca se llame).  
      - Solo se ejecuta una vez por objeto.  
      - Puede "resucitar" objetos y bloquear al Garbage Collector.  
      - Hace el código lento e impredecible.  
      - Está obsoleto en Java moderno.  
    - Alternativa recomendada: usar *`AutoCloseable`* + *try-with-resources*.

# 4. Operadores y sentencias

- **Tipos de operadores:** unario, binario y ternario + pueden aplicarse a uno, dos o tres operandos.
  | Operador                        | Símbolos y ejemplos                                |
  |---------------------------------|----------------------------------------------------|
  | Operadores post-unarios          | Expresión++, Expresión--                           |
  | Operadores pre-unarios           | ++Expresión, --Expresión                           |
  | Operadores unarios               | +, -, !                                           |
  | Multiplicación, División, Módulo | *, /, %                                           |
  | Suma, Resta                      | +, -                                              |
  | Operadores de cambio             | <<, >>, >>>                                       |
  | Operadores relacionales          | <, >, <=, >=, instanceof                          |
  | Igual, Distinto                  | ==, !=                                            |
  | Operadores lógicos               | &, ^, \|                                          |
  | Operadores lógicos de cortocircuito | &&, \|\|                                       |
  | Operadores ternarios             | Expresión booleana ? expresión1 : expresión2      |
  | Operadores de asignación         | =, +=, -=, *=, /=, %=, &=, ^=, !=, <<=, >>=, >>>= |













