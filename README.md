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
        String ced, nam, cargo, tel, salfm, comisiones;

        try {
            FileWriter outFile = new FileWriter(file_name + ".txt", false);
            PrintWriter register_clientes = new PrintWriter(outFile);

            String hay_cliente;
            System.out.println("Hay mas registros? si - no");
            hay_cliente = sc.nextLine();
            while (hay_cliente.equalsIgnoreCase("si")) {
                System.out.println("Ingrese Cedula");
                ced = sc.nextLine();
                System.out.println("Ingrese Nombre");
                nam = sc.nextLine();
                System.out.println("Ingrese Cargo");
                cargo = sc.nextLine();
                System.out.println("Ingrese Teléfono");
                tel = sc.nextLine();
                System.out.println("Ingrese Salario Fijo Mensual");
                salfm = sc.nextLine();
                System.out.println("Ingrese Comisiones");
                comisiones = sc.nextLine();

                while (Double.parseDouble(salfm) < 0) {  // Corregido: debe ser salfm en lugar de cargo
                    System.out.println("Salario debe ser positivo");  // Corregido: mensaje
                    salfm = sc.nextLine();
                }
                if (!ced.isEmpty() && !nam.isEmpty() && !cargo.isEmpty() && !tel.isEmpty() && !salfm.isEmpty() && !comisiones.isEmpty()) {
                    register_clientes.println(ced + "\t" + nam + "\t" + cargo + "\t" + tel + "\t" + salfm + "\t" + comisiones);
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
                cedula = Integer.parseInt(sc.nextLine());  // Corregido: Convertir a entero
                System.out.println("Ingrese el tipo de auto (marca)");  // Corregido: eliminado "marca" redundante
                marca = sc.nextLine();
                do {
                    System.out.println("Ingrese el código del auto");
                    cod = Integer.parseInt(sc.nextLine());  // Corregido: Convertir a entero
                } while (codigos.contains(Integer.toString(cod)));  // Corregido: Verificar si el código ya existe
                codigos.add(Integer.toString(cod));  // Agregar el código al conjunto
                System.out.println("Ingrese el precio del carro: ");
                monto = Double.parseDouble(sc.nextLine());  // Corregido: Convertir a double

                if (!name.isEmpty() && !marca.isEmpty() && monto >= 0) {  // Corregido: monto debe ser positivo
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

     
    
      
