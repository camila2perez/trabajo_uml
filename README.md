# trabajo_uml

## 1. Diagrama a código

### diagrama 

![image](https://github.com/user-attachments/assets/c8c1682f-3c61-4c91-8dba-6c6db08dd744)


  
### codigo
```java
// clase
public abstract class Shape {
    public abstract void draw();
    public abstract void erase();
    public abstract void move();
    public abstract void resize();
}

// clase extendida
public class Circle extends Shape {
    private float radius;
    private int center;

    public Circle(float radius, int center) {
        this.radius = radius;
        this.center = center;
    }

    @Override
    public void draw() {
        // Implementación del dibujo del círculo
    }

    @Override
    public void erase() {
        // Implementación para borrar el círculo
    }

    @Override
    public void move() {
        // Implementación para mover el círculo
    }

    @Override
    public void resize() {
        // Implementación para redimensionar el círculo
    }

    public double area(float radius) {
        return Math.PI * radius * radius;
    }

    public double circum() {
        return 2 * Math.PI * radius;
    }

    public void setCenter(int center) {
        this.center = center;
    }

    public void setRadius(float radius) {
        this.radius = radius;
    }
}

public class Rectangle extends Shape {
    @Override
    public void draw() {
        // Implementación para dibujar un rectángulo
    }

    @Override
    public void erase() {
        // Implementación para borrar el rectángulo
    }

    @Override
    public void move() {
        // Implementación para mover el rectángulo
    }

    @Override
    public void resize() {
        // Implementación para redimensionar el rectángulo
    }
}

public class Polygon extends Shape {
    @Override
    public void draw() {
        // Implementación para dibujar un polígono
    }

    @Override
    public void erase() {
        // Implementación para borrar el polígono
    }

    @Override
    public void move() {
        // Implementación para mover el polígono
    }

    @Override
    public void resize() {
        // Implementación para redimensionar el polígono
    }
}

// clase composicion

public class Point {
    private int x;
    private int y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public int getX() {
        return x;
    }

    public void setX(int x) {
        this.x = x;
    }

    public int getY() {
        return y;
    }

    public void setY(int y) {
        this.y = y;
    }
}


// clase window

public class Window {
    public void open() {
        // Código para abrir la ventana
    }

    public void close() {
        // Código para cerrar la ventana
    }

    public void move() {
        // Código para mover la ventana
    }

    public void display() {
        // Código para mostrar la ventana
    }

    public void handleEvent() {
        // Código para manejar eventos
    }
}

public class Frame extends Window {
    // Implementación específica de Frame
}

// clase control y limite 

public class DrawingContext {
    public void setPoint() {
        // Establecer un punto
    }

    public void clearScreen() {
        // Limpiar la pantalla
    }

    public void getVerticalSize() {
        // Obtener el tamaño vertical
    }

    public void getHorizontalSize() {
        // Obtener el tamaño horizontal
    }
}

public class ConsoleWindow extends Window {
    // Implementación de una ventana de consola
}

public class DialogBox extends Window {
    // Implementación de un cuadro de diálogo
}

public class DataController {
    // Clase de control para manejar los datos
}
```

## 2.  Código a diagrama

### codigo 

```java
import java.util.ArrayList;
import java.util.List;
import java.util.Random;

// Clase Ataque
class Ataque {
    private String nombre;
    private int danio;

    public Ataque(String nombre, int danio) {
        this.nombre = nombre;
        this.danio = danio;
    }

    public String getNombre() {
        return nombre;
    }

    public int getDanio() {
        return danio;
    }
}

// Clase Pokemon (base)
class Pokemon {
    private String nombre;
    private int salud;
    private List<Ataque> ataques;

    public Pokemon(String nombre, int salud) {
        this.nombre = nombre;
        this.salud = salud;
        this.ataques = new ArrayList<>();
    }

    public void agregarAtaque(Ataque ataque) {
        ataques.add(ataque);
    }

    public void recibirDanio(int danio) {
        salud -= danio;
        System.out.println(nombre + " ha recibido " + danio + " puntos de daño. Salud restante: " + salud);
    }

    public boolean estaVivo() {
        return salud > 0;
    }

    public String getNombre() {
        return nombre;
    }

    public List<Ataque> getAtaques() {
        return ataques;
    }
}

// Clase Agua (subclase de Pokemon)
class Agua extends Pokemon {
    public Agua(String nombre) {
        super(nombre, 100); // Salud inicial
    }

    @Override
    public void recibirDanio(int danio) {
        // Reducción de daño para tipo agua
        int danioReducido = (int) (danio * 0.8); // 20% de reducción
        super.recibirDanio(danioReducido);
    }
}

// Clase Fuego (subclase de Pokemon)
class Fuego extends Pokemon {
    public Fuego(String nombre) {
        super(nombre, 100); // Salud inicial
    }

    @Override
    public void recibirDanio(int danio) {
        // Aumento de daño para tipo fuego
        int danioAumentado = (int) (danio * 1.2); // 20% de aumento
        super.recibirDanio(danioAumentado);
    }
}

// Clase Electrico (subclase de Pokemon)
class Electrico extends Pokemon {
    public Electrico(String nombre) {
        super(nombre, 100); // Salud inicial
    }

    @Override
    public void recibirDanio(int danio) {
        // Pokémon de tipo eléctrico puede absorber un 10% del daño como salud
        int danioRecibido = (int) (danio * 0.9); // 10% menos de daño
        super.recibirDanio(danioRecibido);

        // Restaurar un pequeño porcentaje de salud
        int saludRestaurada = (int) (danio * 0.1); // 10% del daño recibido se convierte en salud
        System.out.println(getNombre() + " ha absorbido " + saludRestaurada + " puntos de salud.");
    }
}

// Clase Entrenador
class Entrenador {
    private String nombre;
    private List<Pokemon> pokemons;

    public Entrenador(String nombre) {
        this.nombre = nombre;
        this.pokemons = new ArrayList<>();
    }

    public void agregarPokemon(Pokemon pokemon) {
        pokemons.add(pokemon);
    }

    public Pokemon elegirPokemon() {
        // Elige un Pokémon al azar de la lista
        Random rand = new Random();
        return pokemons.get(rand.nextInt(pokemons.size()));
    }

    public String getNombre() {
        return nombre;
    }
}

// Clase Batalla
class Batalla {
    public static void main(String[] args) {
        // Crear ataques
        Ataque ataqueAgua = new Ataque("Chorro de Agua", 15);
        Ataque ataqueFuego = new Ataque("Llamarada", 20);
        Ataque ataqueElectrico = new Ataque("Impactrueno", 18);

        // Crear Pokémon
        Pokemon squirtle = new Agua("Squirtle");
        squirtle.agregarAtaque(ataqueAgua);
        Pokemon charizard = new Fuego("Charizard");
        charizard.agregarAtaque(ataqueFu
```
### diagrama 

![image](https://github.com/user-attachments/assets/8f40528b-8d00-4eca-84e0-f3c2796bcdc2)


## Código de Proyecto

``` java
import java.util.ArrayList;
import java.util.List;

// Clase Almuerzo (Base)
class Almuerzo {
    private String nombre;
    private double precio;

    public Almuerzo(String nombre, double precio) {
        this.nombre = nombre;
        this.precio = precio;
    }

    public String getNombre() {
        return nombre;
    }

    public double getPrecio() {
        return precio;
    }
}

// Subclase AlmuerzoVegetariano hereda de Almuerzo
class AlmuerzoVegetariano extends Almuerzo {
    public AlmuerzoVegetariano() {
        super("Almuerzo Vegetariano", 5.00); // Precio fijo para el almuerzo vegetariano
    }
}

// Subclase AlmuerzoNoVegetariano hereda de Almuerzo
class AlmuerzoNoVegetariano extends Almuerzo {
    public AlmuerzoNoVegetariano() {
        super("Almuerzo No Vegetariano", 6.50); // Precio fijo para el almuerzo no vegetariano
    }
}

// Clase Pedido que contiene asociación con la clase Almuerzo
class Pedido {
    private Estudiante estudiante;
    private Almuerzo almuerzo;
    private String estado;

    public Pedido(Estudiante estudiante, Almuerzo almuerzo) {
        this.estudiante = estudiante;
        this.almuerzo = almuerzo;
        this.estado = "Pendiente";
    }

    public void marcarComoEntregado() {
        estado = "Entregado";
    }

    public String getEstado() {
        return estado;
    }

    public Estudiante getEstudiante() {
        return estudiante;
    }

    public Almuerzo getAlmuerzo() {
        return almuerzo;
    }

    public void mostrarPedido() {
        System.out.println("Estudiante: " + estudiante.getNombre());
        System.out.println("Almuerzo: " + almuerzo.getNombre());
        System.out.println("Estado: " + estado);
    }
}

// Clase Estudiante (Composición con Pedido)
class Estudiante {
    private String nombre;
    private String matricula;

    public Estudiante(String nombre, String matricula) {
        this.nombre = nombre;
        this.matricula = matricula;
    }

    public String getNombre() {
        return nombre;
    }

    public String getMatricula() {
        return matricula;
    }
}

// Clase Cafeteria que maneja los pedidos
class Cafeteria {
    private List<Pedido> pedidos;

    public Cafeteria() {
        pedidos = new ArrayList<>();
    }

    public void recibirPedido(Pedido pedido) {
        pedidos.add(pedido);
        System.out.println("Pedido recibido de: " + pedido.getEstudiante().getNombre() + " para el almuerzo: " + pedido.getAlmuerzo().getNombre());
    }

    public void entregarPedido(Pedido pedido) {
        pedido.marcarComoEntregado();
        System.out.println("Pedido entregado a: " + pedido.getEstudiante().getNombre());
    }

    public void mostrarPedidos() {
        for (Pedido pedido : pedidos) {
            pedido.mostrarPedido();
            System.out.println("----------------------------");
        }
    }
}

// Clase Principal para probar el sistema
public class Main {
    public static void main(String[] args) {
        // Crear la cafetería
        Cafeteria cafeteria = new Cafeteria();

        // Crear estudiantes
        Estudiante estudiante1 = new Estudiante("Juan Pérez", "A001");
        Estudiante estudiante2 = new Estudiante("Ana López", "B002");

        // Crear almuerzos
        Almuerzo almuerzoVegetariano = new AlmuerzoVegetariano();
        Almuerzo almuerzoNoVegetariano = new AlmuerzoNoVegetariano();

        // Crear pedidos
        Pedido pedido1 = new Pedido(estudiante1, almuerzoVegetariano);
        Pedido pedido2 = new Pedido(estudiante2, almuerzoNoVegetariano);

        // Recibir pedidos en la cafetería
        cafeteria.recibirPedido(pedido1);
        cafeteria.recibirPedido(pedido2);

        // Mostrar todos los pedidos
        System.out.println("----- Lista de pedidos -----");
        cafeteria.mostrarPedidos();

        // Entregar un pedido
        System.out.println("\nEntregando pedido de Ana López...");
        cafeteria.entregarPedido(pedido2);

        // Mostrar estado de los pedidos después de entregar
        System.out.println("\n----- Estado de los pedidos -----");
        cafeteria.mostrarPedidos();
    }
}
``` 
## diagrama en uml 

![image](https://github.com/user-attachments/assets/c0a289fe-4dbb-48aa-aa7f-58210be68436)

