## Modelo vista controlador
Es un patron de diseno de software que separa una aplicacion en tres componentes interracionados. Este patron ayuda a organizar el codigo de manera
que sea mas modular, manteniendo la logica de la aplicacion y la interfaz grafica separadas.

Componentes de MVC:
Modelo (Model):

Qué es?: El modelo es la parte de la aplicación que maneja la lógica de los datos y las reglas de negocio. Es responsable de almacenar y gestionar la información.
Ejemplo: Si estuviéramos creando una aplicación de gestión de estudiantes, el modelo sería la clase que maneja los datos del estudiante (nombre, matrícula, calificaciones, etc.).
Vista (View):

Qué es?: La vista es la parte de la aplicación que se encarga de mostrar los datos al usuario. Generalmente, la vista es la interfaz gráfica o los formularios que el usuario utiliza para interactuar con la aplicación.
Ejemplo: En un programa de Java Swing, los botones, etiquetas y cuadros de texto son parte de la vista.
Controlador (Controller):

Qué es?: El controlador actúa como intermediario entre el modelo y la vista. Recibe las entradas del usuario (a través de la vista), las procesa y actualiza el modelo. También puede actualizar la vista cuando los datos del modelo cambian.
Ejemplo: Si el usuario hace clic en un botón para guardar los datos de un estudiante, el controlador es responsable de tomar esa acción, comunicarse con el modelo y luego actualizar la vista.

Ejemplo: Modelo -> Student.java

```Java
public class Student {
    private String name;
    private int age;

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Getters y Setters
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```
Vista: StudentView.java
```java
import javax.swing.*;
import java.awt.*;

public class StudentView extends JFrame {
    private JTextField nameField = new JTextField(20);
    private JTextField ageField = new JTextField(20);
    private JButton saveButton = new JButton("Guardar");

    public StudentView() {
        // Configuración de la ventana
        setTitle("Formulario de Estudiante");
        setLayout(new GridLayout(3, 2));

        // Agregar los componentes al formulario
        add(new JLabel("Nombre:"));
        add(nameField);
        add(new JLabel("Edad:"));
        add(ageField);
        add(saveButton);

        // Configurar tamaño y visibilidad
        pack();
        setVisible(true);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    }

    // Métodos para obtener los datos del formulario
    public String getStudentName() {
        return nameField.getText();
    }

    public int getStudentAge() {
        return Integer.parseInt(ageField.getText());
    }

    public JButton getSaveButton() {
        return saveButton;
    }
}
```

controller: StudentController.java

```Java
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class StudentController {
    private Student model;
    private StudentView view;

    public StudentController(Student model, StudentView view) {
        this.model = model;
        this.view = view;

        // Añadir el ActionListener al botón guardar
        this.view.getSaveButton().addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                model.setName(view.getStudentName());
                model.setAge(view.getStudentAge());
                JOptionPane.showMessageDialog(null, "Datos Guardados: " +
                        "\nNombre: " + model.getName() +
                        "\nEdad: " + model.getAge());
            }
        });
    }
}
```
Main.java
```java
public class Main {
    public static void main(String[] args) {
        // Crear el modelo
        Student student = new Student("", 0);

        // Crear la vista
        StudentView view = new StudentView();

        // Crear el controlador
        StudentController controller = new StudentController(student, view);
    }
}
```
Modelo (Student.java): Aquí almacenamos el nombre y la edad del estudiante.
Vista (StudentView.java): Esta clase es responsable de mostrar el formulario al usuario y obtener los datos introducidos en los campos de texto.
Controlador (StudentController.java): Actúa como intermediario, toma la información de la vista (cuando el usuario hace clic en el botón "Guardar") y actualiza el modelo con los datos del estudiante.

## Cookie-recipe-java usando el patron MVC

Melany tiene una idea de negocio basada en su habilidad para cocinar deliciosas galletas, utilizando una receta especial de su familia. Sus galletas son tan buenas que todo el mundo que las prueba asegura que son las mejores que han comido.

Melany cuenta con un presupuesto inicial de 15,000 pesos para comenzar su negocio de venta de galletas por docenas. Ella decide compartir su idea con sus amigas Aline y Sofía, quienes también están dispuestas a invertir 15,000 pesos cada una, a cambio de una parte igual de las ganancias.

Las tres amigas tienen claro que necesitan asegurarse de que su inversión será rentable y que las ganancias podrán dividirse de manera justa entre ellas. Para hacer esto, necesitan calcular cuántas docenas de galletas pueden producir con su presupuesto y cuánto deben cobrar por cada docena para obtener ganancias.

Además, saben que necesitarán comprar ingredientes para producir las galletas, por lo que Sofía sugiere a sus amigos Juan y José, quienes les ofrecen los siguientes precios para los ingredientes que necesitarán por cada docena de galletas:

Harina (kg): 20 pesos
Azúcar (kg): 15 pesos
Huevos (unidad): 3 pesos
Mantequilla (kg): 50 pesos
Leche (litro): 12 pesos
Ingrediente secreto (kg): 5 pesos
Aline, pensando en cómo organizar mejor los cálculos financieros, le pide a su amigo Julio, que es programador, que desarrolle un programa para ayudarlas a calcular los costos de producción y las ganancias por cada docena vendida. Julio acepta hacer el programa a cambio del 10% de las ganancias de la primera venta.

Objetivo: Implementar un programa utilizando el patrón MVC (Modelo-Vista-Controlador) que permita a las amigas calcular:

El costo de producir una docena de galletas.
Cuántas docenas pueden producir con su presupuesto inicial.
El precio de venta por docena para obtener un porcentaje de ganancia.
Las ganancias totales y las ganancias para cada una de las amigas.
Cuántas docenas necesitan vender para recuperar su inversión.
Requerimientos:
Modelo (Model):

Crear una clase Ingrediente que contenga:
Un constructor public Ingrediente(String nombre, double precioPorUnidad) que reciba el nombre y el precio del ingrediente.
Crear una clase Negocio que contenga:
Un constructor public Negocio(double presupuesto, Ingrediente[] ingredientes, double[] cantidadesPorDocena) que reciba el presupuesto inicial, un arreglo de ingredientes, y las cantidades necesarias por docena.
Métodos para:
calcularCostoPorDocena(): que calcule el costo de producir una docena de galletas.
calcularDocenasPosibles(double costoPorDocena): que calcule cuántas docenas pueden producir con el presupuesto.
calcularPrecioVenta(double costoPorDocena, double porcentajeGanancia): que calcule el precio de venta por docena para obtener un porcentaje de ganancia.
calcularGananciasTotales(int docenasPosibles, double precioVentaPorDocena, double costoPorDocena): que calcule las ganancias totales.
calcularDocenasParaRecuperarInversion(double presupuesto, double precioVentaPorDocena): que calcule cuántas docenas necesitan vender para recuperar su inversión.
Vista (View):

Crear una clase Vista que interactúe con el usuario para:
Obtener el porcentaje de ganancia que desean agregar.
Obtener cuántas docenas esperan vender en la primera semana.
Mostrar los resultados de los cálculos, como el costo por docena, precio de venta, cuántas docenas pueden producir, ganancias totales, y cuántas docenas necesitan vender para recuperar la inversión.
Controlador (Controller):

Crear una clase Controlador que coordine la interacción entre el modelo (Negocio) y la vista (Vista).
Clase Principal:

1. Implementar la clase principal CookieBusiness que inicialice:
    - El modelo
    - Vista
    - Controlador
   
Utilizar los objetos creados para realizar los cálculos y mostrar los resultados.
2. Utilizar el metodo redondearDosDecimales para mostrar los resultados con dos decimales
3. Separar en archivos diferentes

```Java
// Método auxiliar para redondear a dos decimales
public static double redondearDosDecimales(double valor) {
    return Math.round(valor * 100.0) / 100.0;
}
```
```Java
import java.util.Scanner;

public class CookieBusiness {

    public static void main(String[] args) {
        Ingrediente[] ingredientes = {
            new Ingrediente("Harina (kg)", 20),
            new Ingrediente("Azucar (kg)", 15),
            new Ingrediente("Huevos (unidad)", 3),
            new Ingrediente("Mantequilla (kg)", 50),
            new Ingrediente("Leche (litro)", 12)
        };
        
        double[] cantidadesPorDocena = {0.5, 0.2, 4, 0.1, 0.3};
        double presupuesto = 3000;  

        Negocio negocio = new Negocio(presupuesto, ingredientes, cantidadesPorDocena);
        Vista vista = new Vista();
        Controlador controlador = new Controlador(negocio, vista);

        controlador.iniciar();
    }
}

// Clase Ingrediente
class Ingrediente {
    String nombre;
    double precioPorUnidad;

    public Ingrediente(String nombre, double precioPorUnidad) {
        this.nombre = nombre;
        this.precioPorUnidad = precioPorUnidad;
    }
}

// Clase Negocio
class Negocio {
    double presupuesto;
    Ingrediente[] ingredientes;
    double[] cantidadesPorDocena;
    
    public Negocio(double presupuesto, Ingrediente[] ingredientes, double[] cantidadesPorDocena) {
        this.presupuesto = presupuesto;
        this.ingredientes = ingredientes;
        this.cantidadesPorDocena = cantidadesPorDocena;
    }

    // Calcular el costo por docena
    public double calcularCostoPorDocena() {
        double costo = 0;
        for (int i = 0; i < ingredientes.length; i++) {
            costo += cantidadesPorDocena[i] * ingredientes[i].precioPorUnidad;
        }
        return (costo);
    }

    // Calcular cuantas docenas pueden producir
    public int calcularDocenasPosibles(double costoPorDocena) {
        return (int) (presupuesto / costoPorDocena);
    }

    // Calcular el precio de venta por docena
    public double calcularPrecioVenta(double costoPorDocena, double porcentajeGanancia) {
        return costoPorDocena + (costoPorDocena * (porcentajeGanancia / 100));
    }

    // Calcular las ganancias
    public double calcularGananciasTotales(int docenasPosibles, double precioVentaPorDocena, double costoPorDocena) {
        return (docenasPosibles * precioVentaPorDocena) - (docenasPosibles * costoPorDocena);
    }

    // Calcular cuantas docenas necesitan vender para recuperar la inversion
    public double calcularDocenasParaRecuperarInversion(double presupuesto, double precioVentaPorDocena) {
        return presupuesto / precioVentaPorDocena;
    }
}

class Vista {
    Scanner sc = new Scanner(System.in);

    public double obtenerPorcentajeGanancia() {
        System.out.println("Ingresa el porcentaje de ganancia que deseas agregar sobre el costo de produccion:");
        return sc.nextDouble();
    }

    public int obtenerDocenasVendidas() {
        System.out.println("Ingresa cuantas docenas esperan vender en la primera semana:");
        return sc.nextInt();
    }

    public void mostrarResultados(
        double costoPorDocena, 
        double precioVentaPorDocena, 
        int docenasPosibles, 
        double ingresosTotales, 
        double gananciasTotales, 
        double gananciasPorPersona, 
        double docenasParaRecuperarInversion, 
        double docenasParaGanancias,
        boolean logroObjetivo) {

        System.out.println("\n--- RESULTADOS ---");
        System.out.println("El costo por docena de galletas es de: " + costoPorDocena + " pesos.");
        System.out.println("El precio de venta por docena es de: " + precioVentaPorDocena + " pesos.");
        System.out.println("Pueden producir " + docenasPosibles + " docenas de galletas.");
        System.out.println("Las ganancias totales son: " + gananciasTotales + " pesos.");
        System.out.println("Cada persona recibira " + gananciasPorPersona + " pesos.");
        System.out.println("Para recuperar la inversion deben vender " + (int) docenasParaRecuperarInversion + " docenas.");
        System.out.println("Para obtener ganancias deben vender " + (int) docenasParaGanancias + " docenas.");

        if (logroObjetivo) {
            System.out.println("\nFelicidades Han vendido suficientes docenas para cubrir la inversion y obtener ganancias");
        } else {
            System.out.println("\nLamentablemente, no vendieron suficientes docenas para recuperar la inversion y obtener ganancias");
            System.out.println("Consideren aplicar otra estrategia o dedicarse a otra cosa.");
        }
    }
}

class Controlador {
    private Negocio negocio;
    private Vista vista;

    public Controlador(Negocio negocio, Vista vista) {
        this.negocio = negocio;
        this.vista = vista;
    }

    public void iniciar() {
        double costoPorDocena = negocio.calcularCostoPorDocena();
        double porcentajeGanancia = vista.obtenerPorcentajeGanancia();
        double precioVentaPorDocena = negocio.calcularPrecioVenta(costoPorDocena, porcentajeGanancia);
        
        int docenasPosibles = negocio.calcularDocenasPosibles(costoPorDocena);
        double gananciasTotales = negocio.calcularGananciasTotales(docenasPosibles, precioVentaPorDocena, costoPorDocena);
        double gananciasPorPersona = gananciasTotales / 3;
        double docenasParaRecuperarInversion = negocio.calcularDocenasParaRecuperarInversion(negocio.presupuesto, precioVentaPorDocena);
        double docenasParaGanancias = docenasParaRecuperarInversion * 1.2;

        int docenasVendidas = vista.obtenerDocenasVendidas();
        boolean logroObjetivo = docenasVendidas >= docenasParaGanancias;

        vista.mostrarResultados(
            costoPorDocena, 
            precioVentaPorDocena, 
            docenasPosibles, 
            docenasPosibles * precioVentaPorDocena, 
            gananciasTotales, 
            gananciasPorPersona, 
            docenasParaRecuperarInversion, 
            docenasParaGanancias,
            logroObjetivo
        );
    }
}
```

Salida:
```
Ingresa el porcentaje de ganancia que deseas agregar sobre el costo de produccion:
50
Ingresa cuantas docenas esperan vender en la primera semana:
1000

--- RESULTADOS ---
El costo por docena de galletas es de: 33.6 pesos.
El precio de venta por docena es de: 50.400000000000006 pesos.
Pueden producir 1339 docenas de galletas.
Las ganancias totales son: 22495.200000000004 pesos.
Cada persona recibira 7498.4000000000015 pesos.
Para recuperar la inversion deben vender 892 docenas.
Para obtener ganancias deben vender 1071 docenas.

Lamentablemente, no vendieron suficientes docenas para recuperar la inversion y obtener ganancias
Consideren aplicar otra estrategia o dedicarse a otra cosa.
```

  
