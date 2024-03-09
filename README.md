# Proyecto Java

# Base de Datos (Workbench)

- create database cnel;
- use cnel
- INSERT INTO <clientes> (nombre, apellido, direccion) -> VALUES ('Juan', 'de la Torre', 'Avenida Caracol');
- SELECT * FROM clientes;
- SELECT nombre, apellido FROM clientes;
- SELECT * FROM clientes WHERE id = 2;



# MODELO (CLASS JAVA)

- public class Producto {

      private int id;
      private String codigo;
      private String nombre;
      private Double precio;
  }

  --> insertar código --> Getters y Setters

  ## CONEXION (CLASS JAVA)
'''{
  - private final String db = "tienda";
  - private final String user = "root";
  - private final String password = "1234" or "";
  - private final String url = "jdbc:mysql://localhost:3306/tienda";
  - private Connection con = null;


    public Connection getConexion() {
        try {
          Class.forName("com.mysql.jdbc.Driver");
          con = (Connection) DriverManager.getConnection(this.url, this.user, this.password);
        } catch (SQLException e)
    }
}'''
  # VISTA
  
