# JavaTest

Sistema de inventario en Java
1. Órdenes de pedidos:

Java
public class Orden {

    private String cliente;
    private String fecha;
    private List<Producto> productos;

    public Orden(String cliente, String fecha, List<Producto> productos) {
        this.cliente = cliente;
        this.fecha = fecha;
        this.productos = productos;
    }

    public double total() {
        double total = 0;
        for (Producto producto : productos) {
            total += producto.getPrecio() * producto.getCantidad();
        }
        return total;
    }

    // ... Métodos para registrar la orden en la base de datos

}

public class Producto {

    private String nombre;
    private double precio;
    private int cantidad;

    public Producto(String nombre, double precio, int cantidad) {
        this.nombre = nombre;
        this.precio = precio;
        this.cantidad = cantidad;
    }

    // ... Métodos para obtener y modificar los atributos

}

// Ejemplo de uso
String cliente = "Juan Pérez";
String fecha = "2023-11-14";
List<Producto> productos = Arrays.asList(
    new Producto("Camisa", 10, 1),
    new Producto("Zapatos", 20, 2)
);

Orden orden = new Orden(cliente, fecha, productos);
double total = orden.total();

System.out.println("Total de la orden: " + total);

// Registrar la orden en la base de datos
Usa el código con precaución. Más información
2. Registro de compras:

Java
public class Compra {

    private String proveedor;
    private String fecha;
    private List<Producto> productos;

    public Compra(String proveedor, String fecha, List<Producto> productos) {
        this.proveedor = proveedor;
        this.fecha = fecha;
        this.productos = productos;
    }

    public double total() {
        double total = 0;
        for (Producto producto : productos) {
            total += producto.getPrecio() * producto.getCantidad();
        }
        return total;
    }

    // ... Métodos para registrar la compra en la base de datos

}

// Ejemplo de uso
String proveedor = "Empresa X";
String fecha = "2023-11-14";
List<Producto> productos = Arrays.asList(
    new Producto("Camisa", 10, 1),
    new Producto("Zapatos", 20, 2)
);

Compra compra = new Compra(proveedor, fecha, productos);
double total = compra.total();

System.out.println("Total de la compra: " + total);

// Registrar la compra en la base de datos
Usa el código con precaución. Más información
3. Proveedores:

Java
public class Proveedor {

    private String nombre;
    private String telefono;
    private String correo;

    public Proveedor(String nombre, String telefono, String correo) {
        this.nombre = nombre;
        this.telefono = telefono;
        this.correo = correo;
    }

    // ... Métodos para registrar el proveedor en la base de datos

}

// Ejemplo de uso
String nombre = "Empresa X";
String telefono = "123456789";
String correo = "info@empresax.com";

Proveedor proveedor = new Proveedor(nombre, telefono, correo);

// Registrar el proveedor en la base de datos
Usa el código con precaución. Más información
4. Cardex:

Java
public class Producto {

    private String nombre;
    private double precio;
    private int stock;

    public Producto(String nombre, double precio, int stock) {
        this.nombre = nombre;
        this.precio = precio;
        this.stock = stock;
    }

    public void actualizarStock(int cantidad) {
        // Conectar a la base de datos
        // Actualizar el stock del producto en la base de datos
        this.stock += cantidad;
    }

    // ... Métodos para obtener y modificar los atributos

}

// Ejemplo de uso
Producto producto = new Producto("Camisa", 10, 10);

// Se vende una camisa
producto.actualizarStock(-1);

// Se compra una camisa
producto.actualizarStock(1);
Usa el código con precaución. Más información
5. Categorías:

Java
public class Categoria {

    private String nombre;

    public Categoria(String nombre) {
        this.nombre = nombre;
    }

    // ... Métodos
