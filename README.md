# Proyecto Java

# Base de Datos (Workbench)

- create database cnel;
- use cnel
- INSERT INTO <clientes> (nombre, apellido, direccion) -> VALUES ('Juan', 'de la Torre', 'Avenida Caracol');
- SELECT * FROM clientes;
- SELECT nombre, apellido FROM clientes;
- SELECT * FROM clientes WHERE id = 2;


# CONTROLADOR

## controladorProducto (class java)

            public class ctrlproducto implements ActionListener {

            private Producto mod; (modelo - producto)
            private ConsultasPoducto modC;
            private frmProducto frm; (vista - formulario)

            public ControladorProducto(Producto mod, ConsultasProducto modC, frmProducto frm)
            {
            this.mod=mod;
            this.modC = modC;
            this.frm = frm;
            this.frm.btnGuardar.addActionListener(this);
            this.frm.btnModificar.addActionListener(this);
            this.frm.btnEliminar.addActionListener(this);
            this.frm.btnLimpiar.addActionListener(this);
            this.frm.btnBuscar.addActionListener(this);
            }

            public void iniciar()
            {
            frm.setTitle("Productos");
            frm.setLocationRelativeTo(null);
            frm.txtId.setVisible(false);
            }

            @Override
            public void ActionPerfomed(ActionEvent e) {

guardar

            if (e.getSource() == frm.btnGuardar){
            mod.setCodigo(frm.txtCodigo.getText());
      mod.setPrecio(Double.parseDouble(frm.txtPrecio.getText()));
            if(modC.registrar(mod))
            {
            JOptionPane.showMessageDialog(null, "Registro Exitoso");
            limpiar();
            } else {
            JOptionPane.showMessageDialog(null, "Registro Fallido");
            limpiar();
            }
            }

modificar

            if (e.getSource() == frm.btnModificar){
            mod.setId(Integer.parseInt(frm.txtId.getText()));
            mod.setCodigo(frm.txtCodigo.getText());
            mod.setPrecio(Double.parseDouble(frm.txtPrecio.getText()));
            if(modC.modificar(mod))
            {
            JOptionPane.showMessageDialog(null, "Registro Modificado");
            limpiar();
            } else {
            JOptionPane.showMessageDialog(null, "Modificacion Fallido");
            limpiar();
            }
            }

Eliminar

            if (e.getSource() == frm.btnEliminar){
            mod.setId(Integer.parseInt(frm.txtId.getText()));
            if(modC.eliminar(mod))
            {
            JOptionPane.showMessageDialog(null, "Registro Eliminado");
            limpiar();
            } else {
            JOptionPane.showMessageDialog(null, "Modificacion Eliminado");
            limpiar();
            }
            }


Buscar

            if (e.getSource() == frm.btnBuscar){
            mod.seCodigo(frm.txtCodigo.getText()));
            if(modC.buscar(mod))
            {
            frm.textId.setText(String.valueOf(mod.getId)));
            frm.txtCodigo.setText(mod.getCodigo());
            frm.txtPrecio.setText(String.valueOf(mod.getPrecio()));
            } else {
            JOptionPane.showMessageDialog(null, "No se encontro registro");
            limpiar();
            }
            }

            if (e.getSource() == frmbtnLimpiar){
            limpiar();
            }

            
            }


            public void limpiar(){
            frm.txtId.setText(null);
            frm.txtCodigo.setText(null);
            }

            
            
            }


## CRUDMVC (class java)

            public class CRUDMVC {
                  public static void main(String[] arg){

                  Producto mod = new Producto();
                  ConsultasProducto modC = new ConsultasProducto();
                  frmProducto frm = frmProducto();

                  ControladorProducto ctrl = new ControladorProducto(mod, modC, frm);
                  ctrl.iniciar();
                  frm.setVisible(true);
                  }
            }




# MODELO 

## Producto (CLASS JAVA)

    public class Producto {

      private int id;
      private String codigo;
      private String nombre;
      private Double precio;
    }

    --> insertar código --> Getters y Setters

  ## CONEXION (CLASS JAVA)
 
       {
         private final String db = "tienda";
         private final String user = "root";
         private final String password = "1234" or "";
         private final String url = "jdbc:mysql://localhost:3306/tienda";
         private Connection con = null;


          public Connection getConexion() {
              try {
                Class.forName("com.mysql.jdbc.Driver");
                con = (Connection)                   DriverManager.getConnection(this.url, this.user, this.password);
              } catch (SQLException e)
              {
                    System.err.println(e); 
              } catch (ClassNotFoundExcepton ex) {
                    Logger.getLogger(Conexion.class.getName()).log(Level.SEVERE, null, ex);
              }
                    return con;
              }
         }

## Consultas producto

            public class consultasProducto extends Conexion {
registrar    
                  
                  public boolean registrar (Producto pro) {
                        PreparedStatement ps = null;
                        Connection con = getConexion();

                        String sql = "INSERT INTO producto (codigo, nombre) VALUES (?,?)";
                        try{
                        ps = con.prepareStatement(sql);
                        ps.setString(1, pro.getCodigo());
                        ps.setString(2, pro.getNombre());
                        ps.execute();
                        return true;
                        } catch (SQLException e){
                              System.err.println(e);
                              return false;
                        } finally {
                              try {
                                    con.close();
                              } catch (SQLException e) {
                                    System.err.println(e);
                              }
                        }
                  }


modificar

                  public boolean modificar (Producto pro) {
                        PreparedStatement ps = null;
                        Connection con = getConexion();

                        String sql = "UPDATE producto SET codigo=?, nomre=? WHERE id=?";
                        try{
                        ps = con.prepareStatement(sql);
                        ps.setString(1, pro.getCodigo());
                        ps.setString(2, pro.getNombre());
                        ps.setInt(3, pro.getId());
                        ps.execute();
                        return true;
                        } catch (SQLException e){
                              System.err.println(e);
                              return false;
                        } finally {
                              try {
                                    con.close();
                              } catch (SQLException e) {
                                    System.err.println(e);
                              }
                        }
                  }


ELIMINAR

            public boolean eliminar (Producto pro) {
                        PreparedStatement ps = null;
                        Connection con = getConexion();

                        String sql = "DELETE FROM producto WHERE id=?";
                        try{
                        ps = con.prepareStatement(sql);
                        ps.setInt(1, pro.getId());
                        ps.execute();
                        return true;
                        } catch (SQLException e){
                              System.err.println(e);
                              return false;
                        } finally {
                              try {
                                    con.close();
                              } catch (SQLException e) {
                                    System.err.println(e);
                              }
                        }
                  }


BUSCAR 


            public boolean buscar (Producto pro) {
                        PreparedStatement ps = null;
                        ResultSet rs = null;
                        Connection con = getConexion();

                        String sql = "SELECT * FROM producto WHERE codigo=?";
                        try{
                        ps = con.prepareStatement(sql);
                        ps.setString(1, pro.getCodigo());
                        ps.execute();

                        if(rs.next())
                        {
                                                      pro.setId(Integer.parseInt(rs.getString("id")));
                        pro.setCodigo(rs.getString("codigo"));
                        pro.setNombre(rs.getString(nombre"));
                        pro.setPrecio(Double.parseDouble(rs.getString("precio")));
                        return true
                              
                        }
                        
                        return false;
                        } catch (SQLException e){
                              System.err.println(e);
                              return false;
                        } finally {
                              try {
                                    con.close();
                              } catch (SQLException e) {
                                    System.err.println(e);
                              }
                        }
                  }
            
            }


  # VISTA
  
