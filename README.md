# Laboratorio1Etr
     package zg;
     
     import java.io.BufferedReader;
     import java.io.File;
     import java.io.FileReader;
     import java.io.FileWriter;
     import java.io.IOException;
     import java.io.PrintWriter;
     import java.util.Scanner;
     import java.util.HashSet;
     import java.util.Set;
public class ZGEJ1 {

    public static void Llenar(Scanner sc, String file_name) {
        int cedula;
        String nam, cargo, tel, salfm, comisiones;
        Set<String> nombres = new HashSet<>();  // Usamos un HashSet para almacenar los nombres únicos
        Set<String> telefonos = new HashSet<>();  // Usamos un HashSet para almacenar los teléfonos únicos
        Set<Integer> cedulas = new HashSet<>();  // Usamos un HashSet para almacenar las cédulas únicas

        try {
            FileWriter outFile = new FileWriter(file_name + ".txt", false);
            PrintWriter register_clientes = new PrintWriter(outFile);

            String hay_cliente;
            System.out.println("Hay mas registros? si - no");
            hay_cliente = sc.nextLine();
            
            while (hay_cliente.equalsIgnoreCase("si")) {
                do {
                    System.out.println("Ingrese Cedula: ");
                    cedula = Integer.parseInt(sc.nextLine());  //  Convertir a entero
                } while (cedulas.contains(cedula));  //  Verificar si la cédula ya existe
                cedulas.add(cedula);  // Agregar la cédula al conjunto
                
                do {
                    System.out.println("Ingrese Nombre");
                    nam = sc.nextLine();
                } while (nombres.contains(nam));  //  Verificar si el nombre ya existe
                nombres.add(nam);  // Agregar el nombre al conjunto
                
                System.out.println("Ingrese Cargo");
                cargo = sc.nextLine();
                
                do {
                    System.out.println("Ingrese Teléfono: ");
                    tel = sc.nextLine();
                } while (telefonos.contains(tel));  //  Verificar si el teléfono ya existe
                telefonos.add(tel);  // Agregar el teléfono al conjunto
                
                System.out.println("Ingrese Salario Fijo Mensual");
                salfm = sc.nextLine();
                System.out.println("Ingrese Comisiones");
                comisiones = sc.nextLine();

                while (Double.parseDouble(salfm) < 0) {  // Corregido: debe ser salfm en lugar de cargo
                    System.out.println("Salario debe ser positivo");  // Corregido: mensaje
                    salfm = sc.nextLine();
                }
                
                if (!nam.isEmpty() && !cargo.isEmpty() && !tel.isEmpty() && !salfm.isEmpty() && !comisiones.isEmpty()) {
                    register_clientes.println(cedula + "\t" + nam + "\t" + cargo + "\t" + tel + "\t" + salfm + "\t" + comisiones);
                }
                
                System.out.println("Hay registros? si - no");  // Corregido: mensaje
                hay_cliente = sc.nextLine();
            }
            
            register_clientes.close();
        } catch (IOException ex) {
            System.out.println("Error creando el archivo");
            ex.printStackTrace();
        }
    }

    public static void Archivo_ventas(Scanner sc, String file_namev) {
        String name, marca;
        int cedula, cod;
        double monto;
        Set<String> codigos = new HashSet<>();  // Usamos un HashSet para almacenar los códigos únicos

        try {
            FileWriter outFile = new FileWriter(file_namev + ".txt", false);
            PrintWriter register_ventas = new PrintWriter(outFile);

            String hay_ventas;
            System.out.println("Hay más ventas? si - no");
            hay_ventas = sc.nextLine();
            
            while (hay_ventas.equalsIgnoreCase("si")) {
                System.out.println("Ingrese el nombre");
                name = sc.nextLine();
                System.out.println("Ingrese el número de cedula");
                cedula = Integer.parseInt(sc.nextLine());  //  Convertir a entero
                System.out.println("Ingrese el tipo de auto (marca)");
                marca = sc.nextLine();
                
                do {
                    System.out.println("Ingrese el código del auto");
                    cod = Integer.parseInt(sc.nextLine());  //  Convertir a entero
                } while (codigos.contains(Integer.toString(cod)));  //  Verificar si el código ya existe
                codigos.add(Integer.toString(cod));  // Agregar el código al conjunto
                
                System.out.println("Ingrese el precio del carro: ");
                monto = Double.parseDouble(sc.nextLine());  //  Convertir a double

                if (!name.isEmpty() && !marca.isEmpty() && monto >= 0) {  //  monto debe ser positivo
                    register_ventas.println(name + "\t" + cedula + "\t" + marca + "\t" + cod + "\t" + monto);
                }
                
                System.out.println("Hay más ventas? si - no");
                hay_ventas = sc.nextLine();
            }
            
            register_ventas.close();
        } catch (IOException ex) {
            System.out.println("Error creando el archivo");
            ex.printStackTrace();
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.println("Ingresar informacion de empleados");
        Llenar(sc, "Empleados");

        System.out.println("Digite nombre del archivo de ventas:");
        String file_namev = sc.nextLine();
        System.out.println("Se llama a funcion Archivo_ventas");
        Archivo_ventas(sc, file_namev);

        sc.close();
    }
}


     
    
      
