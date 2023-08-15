# Laboratorio1Etr
     package zg;
     
     import java.io.BufferedReader;
     import java.io.File;
     import java.io.FileReader;
     import java.io.FileWriter;
     import java.io.IOException;
     import java.io.PrintWriter;
     import java.util.Scanner;

     
     public class ZGEJ1 {

    
    public static void Llenar(Scanner sc, String file_name){
        String ced, nam, cargo,tel,salfm,comisiones;
       //Prueba
        try {
            
            FileWriter outFile = new FileWriter(file_name + ".txt", false);  //Archivo.txt //Crea un archivo en la misma carpeta
            // if false the file will be deleted and created everytime
            // if true the registers will be appended to the end of the file
            PrintWriter register_clientes = new PrintWriter(outFile);
            
            // LOGICA
            String hay_cliente;
            System.out.println("Hay mas registros? si - no");
            hay_cliente = sc.nextLine();
            while(hay_cliente.equalsIgnoreCase("si")){
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
                
                while(Double.parseDouble(cargo) < 0){
                    System.out.println("Saldo debe ser positivo");
                    cargo = sc.nextLine();
                }
                if (!ced.isEmpty() && !nam.isEmpty() && !cargo.isEmpty()&& !tel.isEmpty() && !salfm.isEmpty() && !comisiones.isEmpty()){
                    register_clientes.println(ced+"\t"+ nam +"\t"+ cargo +"\t"+ tel+ "\t" +salfm+ "\t" +comisiones );
                }
                System.out.println("Hay registos? si - no");
                hay_cliente = sc.nextLine();  
            }
           register_clientes.close();
        } catch (IOException ex) {
            System.out.println("Error creando el archivo");
            ex.printStackTrace();
        }
    
    }
    

    
    public static void main(String[] args) {
        // TODO code application logic here
        Scanner sc = new Scanner(System.in);
        
        //System.out.println("Digite nombre del archivo");
        //String file_name = sc.nextLine(); // Archivo
        //System.out.println("Se llama a funcion crear o llenar archivo");
        System.out.println("Ingresar informacion de empleados");
        Llenar(sc, "Empleados");
        
        //System.out.println("Llenar informacion de transacciones");
        //Llenar(sc, "Transacciones");
        //System.out.println("¿Qué archivo desea abrir?");
        //String file_name = sc.nextLine();
        //Leer(sc, file_name);
        //Update_stuff("Clientes",  "Transacciones");
        sc.close();
    }
    
     }
