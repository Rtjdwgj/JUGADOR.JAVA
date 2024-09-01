# JUGADOR.JAVA  
import java.util.ArrayList;
import java.util.Scanner;

/**
 * Clase principal que maneja un sistema de gestión de jugadores.
 * Permite agregar, eliminar, buscar, editar y listar jugadores.
 */
public class Main {
    private static ArrayList<Jugador> jugadores = new ArrayList<>();
    private static int idActual = 1;

    /**
     * Método principal que inicia el programa.
     * Presenta un menú de opciones para interactuar con el sistema.
     * 
     * @param args Argumentos de la línea de comandos (no utilizados).
     */
    public static void main(final String[] args) {
        final Scanner scanner = new Scanner(System.in);
        while (true) {
            System.out.println("Menú:");
            System.out.println("1. Agregar jugador");
            System.out.println("2. Eliminar jugador");
            System.out.println("3. Buscar jugador");
            System.out.println("4. Editar jugador");
            System.out.println("5. Listar jugadores");
            System.out.println("6. Salir");
            System.out.print("Ingrese la opción: ");
            final int opcion = scanner.nextInt();
            switch (opcion) {
                case 1:
                    agregarJugador(scanner);
                    break;
                case 2:
                    eliminarJugador(scanner);
                    break;
                case 3:
                    buscarJugador(scanner);
                    break;
                case 4:
                    editarJugador(scanner);
                    break;
                case 5:
                    listarJugadores();
                    break;
                case 6:
                    System.out.println("Adiós!");
                    return;
                default:
                    System.out.println("Opción inválida");
            }
        }
    }

    /**
     * Lista todos los jugadores registrados en el sistema.
     * Si no hay jugadores, muestra un mensaje indicando que no hay jugadores registrados.
     */
    private static void listarJugadores() {
        if (jugadores.isEmpty()) {
            System.out.println("No hay jugadores registrados.");
        } else {
            System.out.println("Lista de jugadores:");
            for (Jugador jugador : jugadores) {
                System.out.println(jugador);
            }
        }
    }

    /**
     * Agrega un nuevo jugador al sistema.
     * Solicita al usuario el nombre, apellido y edad del jugador.
     * 
     * @param scanner El escáner utilizado para leer la entrada del usuario.
     */
    private static void agregarJugador(final Scanner scanner) {
        System.out.print("Ingrese el nombre del jugador: ");
        final String nombre = scanner.next();
        System.out.print("Ingrese el apellido del jugador: ");
        final String apellido = scanner.next();
        System.out.print("Ingrese la edad del jugador: ");
        final int edad = scanner.nextInt();
        final Jugador jugador = new Jugador(idActual, nombre, apellido, edad);
        jugadores.add(jugador);
        idActual++;
        System.out.println("Jugador agregado con éxito!");
        listarJugadores();
    }

    /**
     * Elimina un jugador del sistema.
     * Solicita al usuario el ID del jugador a eliminar y confirma la eliminación.
     * 
     * @param scanner El escáner utilizado para leer la entrada del usuario.
     */
    private static void eliminarJugador(final Scanner scanner) {
        System.out.print("Ingrese el ID del jugador a eliminar: ");
        final int id = scanner.nextInt();
        final Jugador jugador = buscarjugadorporId(id);
        if (jugador != null) {
            System.out.println("¿Está seguro de eliminar al jugador " + jugador.getNombre() + "? (si/no)");
            final String respuesta = scanner.next();
            if (respuesta.equalsIgnoreCase("s")) {
                jugadores.remove(jugador);
                System.out.println("Jugador eliminado con éxito!");
                listarJugadores();
            } else {
                System.out.println("Operación cancelada");
            }
        } else {
            System.out.println("Jugador no encontrado");
        }
    }

    /**
     * Busca un jugador por su ID.
     * 
     * @param id El ID del jugador a buscar.
     * @return El jugador si es encontrado, null en caso contrario.
     */
    private static Jugador buscarjugadorporId(int id) {
        for (Jugador jugador : jugadores) {
            if (jugador.getId() == id) {
                return jugador;
            }
        }
        return null;
    }

    /**
     * Busca un jugador en el sistema.
     * Solicita al usuario el ID del jugador a buscar y muestra su información si es encontrado.
     * 
     * @param scanner El escáner utilizado para leer la entrada del usuario.
     */
    private static void buscarJugador(final Scanner scanner) {
        System.out.print("Ingrese el ID del jugador a buscar: ");
        final int id = scanner.nextInt();
        final Jugador jugador = buscarjugadorporId(id);
        if (jugador != null) {
            System.out.println(jugador.toString());
        } else {
            System.out.println("Jugador no encontrado");
        }
    }

    /**
     * Edita la información de un jugador en el sistema.
     * Solicita al usuario el ID del jugador y los nuevos datos a modificar.
     * 
     * @param scanner El escáner utilizado para leer la entrada del usuario.
     */
    private static void editarJugador(final Scanner scanner) {
        System.out.print("Ingrese el ID del jugador a editar: ");
        int id = scanner.nextInt();
        Jugador jugador =  buscarjugadorporId(id);
        if (jugador != null) {
            System.out.println("Ingrese el nuevo nombre del jugador: ");
            String nombre = scanner.next();
            System.out.println("Ingrese el nuevo apellido del jugador: ");
            String apellido = scanner.next();
            System.out.println("Ingrese la nueva edad del jugador: ");
            int edad = scanner.nextInt();
            jugador.setNombre(nombre);
            jugador.setApellido(apellido);
            jugador.setEdad(edad);
            System.out.println("Jugador editado con éxito!");
            listarJugadores();
        } else {
            System.out.println("Jugador no encontrado");
        }
    }
}

/**
 * Clase que representa un jugador.
 * Contiene los datos del jugador como ID, nombre, apellido y edad.
 */
class Jugador {
    private int id;
    private String nombre;
    private String apellido;
    private int edad;

    /**
     * Constructor de la clase Jugador.
     * 
     * @param id El ID del jugador.
     * @param nombre El nombre del jugador.
     * @param apellido El apellido del jugador.
     * @param edad La edad del jugador.
     */
    public Jugador(int id, String nombre, String apellido, int edad) {
        this.id = id;
        this.nombre = nombre;
        this.apellido = apellido;
        this.edad = edad;
    }

    // Getters y Setters
    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getNombre() {
        return nombre;
    }

    public void setNombre(String nombre) {
        this.nombre = nombre;
    }

    public String getApellido() {
        return apellido;
    }

    public void setApellido(String apellido) {
        this.apellido = apellido;
    }

    public int getEdad() {
        return edad;
    }

    public void setEdad(int edad) {
        this.edad = edad;
    }

    @Override
    public String toString() {
        return "Jugador{" +
                "id=" + id +
                ", nombre='" + nombre + '\'' +
                ", apellido='" + apellido + '\'' +
                ", edad=" + edad +
                '}';
    }
}
