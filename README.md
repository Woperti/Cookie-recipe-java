# Cookie-recipe-java
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

  
