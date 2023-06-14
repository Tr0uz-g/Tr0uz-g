- 👋 Hi, I’m @Tr0uz-g
//////////////////////////////////////////////////////////////////Servidor.Java/////////////////////////////////////////////////////////

import java.io.*;
import java.net.*;

public class Servidor {
    public static void main(String[] args) {
        try {
            // Crear un ServerSocket que escucha en el puerto 12345
            ServerSocket serverSocket = new ServerSocket(12345);

            System.out.println("Esperando conexiones entrantes...");

            // Esperar a que un cliente se conecte
            Socket clientSocket = serverSocket.accept();

            System.out.println("Cliente conectado: " + clientSocket.getInetAddress());

            // Crear un BufferedReader para leer los datos booleanos del cliente
            DataInputStream input = new DataInputStream(clientSocket.getInputStream());

            // Leer y mostrar los datos booleanos del cliente
            boolean value1 = input.readBoolean();
            boolean value2 = input.readBoolean();
            System.out.println("Valor 1: " + value1);
            System.out.println("Valor 2: " + value2);

            // Cerrar las conexiones y liberar los recursos
            input.close();
            clientSocket.close();
            serverSocket.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

//////////////////////////////////////////////////////////////////Cliente.java/////////////////////////////////////////////////////////

import java.io.*;
import java.net.*;

public class Cliente {
    public static void main(String[] args) {
        try {
            // Crear un Socket y establecer la conexión con el servidor en el puerto 12345
            Socket socket = new Socket("localhost", 12345);

            // Crear un DataOutputStream para enviar los datos booleanos al servidor
            DataOutputStream output = new DataOutputStream(socket.getOutputStream());

            // Enviar los valores booleanos al servidor
            output.writeBoolean(true);
            output.writeBoolean(false);

            // Cerrar la conexión y liberar los recursos
            output.close();
            socket.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}


