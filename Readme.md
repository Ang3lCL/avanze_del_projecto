## Avance del proyecto

**Enunciado**  
aqui se creo un sistema de biblioteca que tiene lo siguiente:
Debe permitir registrar y consultar libros, usuarios y préstamos.
Debe validar que los datos ingresados sean correctos y coherentes.
Debe controlar que no se presten más libros de los que hay disponibles ni que se exceda el límite de dos ejemplares por usuario.
Debe generar reportes (impresiones en pantalla) sobre el estado de la biblioteca, así como del número de libros, usuarios y préstamos.

**Codigo**  
````java
package avanze_del_project;

import java.util.Scanner;

class Libro {
    private String titulo;
    private String autor;
    private String genero;
    private int año;
    private int totalCopias;
    private int copiasPrestadas;

    public Libro(String titulo, String autor, String genero, int año, int totalCopias) {
        this.titulo = titulo;
        this.autor = autor;
        this.genero = genero;
        this.año = año;
        this.totalCopias = totalCopias;
        this.copiasPrestadas = 0;
    }

    public String getTitulo() {
        return titulo;
    }

    public int getCopiasDisponibles() {
        return totalCopias - copiasPrestadas;
    }

    public boolean prestar() {
        if (getCopiasDisponibles() > 0) {
            copiasPrestadas++;
            return true;
        }
        return false;
    }

    public boolean devolver() {
        if (copiasPrestadas > 0) {
            copiasPrestadas--;
            return true;
        }
        return false;
    }

    @Override
    public String toString() {
        return "Título: " + titulo +
                "\nAutor: " + autor +
                "\nGénero: " + genero +
                "\nAño: " + año +
                "\nCopias totales: " + totalCopias +
                "\nPrestadas: " + copiasPrestadas +
                "\nDisponibles: " + getCopiasDisponibles();
    }
}

class Cliente {
    String nombre;
    int edad;
    int id;
    int librosPrestados;


    public Cliente(String nombre, int edad, int id) {
        this.nombre = nombre;
        this.edad = edad;
        this.id = id;
        this.librosPrestados = 0;
    }

    public Cliente() {
        this.librosPrestados = 0;
    }

}

public class avance_projecto {

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);


        Cliente[] usuarios = new Cliente[10];
        int totalUsuarios = 0;
        Cliente usuarioActual = null;


        Libro libro1 = new Libro("El Señor de los Anillos", "Tolkien", "Fantasía", 1954, 3);
        Libro libro2 = new Libro("Cien años de soledad", "García Márquez", "Novela", 1967, 2);
        Libro libro3 = new Libro("La metamorfosis", "Kafka", "Novela", 1915, 4);
        Libro libro4 = new Libro("La odisea", "Homero", "Epopeya", 700, 2);
        Libro libro5 = new Libro("Estravagario", "Pablo Neruda", "Poesía", 1958, 3);
        Libro libro6 = new Libro("Danza de Dragones", "George R. R. Martin", "Fantasía", 2011, 2);


        System.out.print(" Tienes un usuario? (si/no): ");
        String respuesta = sc.nextLine();

        if (!respuesta.equalsIgnoreCase("si")) {
            System.out.print("Quieres crear un usuario? (si/no): ");
            String crear = sc.nextLine();

            if (crear.equalsIgnoreCase("no")) {
                System.out.println("Regresa pronto");
                System.out.println("Programa terminado.");
                sc.close();
                return;  
            }

            Cliente nuevo = new Cliente();
            System.out.println("Creando nuevo usuario");
            System.out.print("Escribe tu nombre: ");
            nuevo.nombre = sc.nextLine();
            System.out.print("Ingresa tu edad: ");
            nuevo.edad = sc.nextInt();
            System.out.print("Elige un ID de 4 dígitos (ex. 1234): ");
            nuevo.id = sc.nextInt();
            nuevo.librosPrestados = 0;
            sc.nextLine();

            usuarios[totalUsuarios++] = nuevo;
            totalUsuarios++;
            usuarioActual = nuevo;

            System.out.println("Usuario creado");
            System.out.println("Bienvenido " + nuevo.nombre);

        } else if (respuesta.equalsIgnoreCase("si")) {
            
            if (usuarioActual == null) {
                System.out.println("Usuario no encontrado.");
                sc.close();
                return;
            }
        } else if (totalUsuarios == 0) {
                System.out.println("No hay usuarios registrados.");
                sc.close();
                return;
            }
=
        int opcion;
        do {
            System.out.println("\n=== MENÚ BIBLIOTECA ===");
            System.out.println("1. Ver información de los libros");
            System.out.println("2. Pedir prestado un libro");
            System.out.println("3. Devolver un libro");
            System.out.println("4. Ver cantidad de libros que tienes");
            System.out.println("5. Salir");
            System.out.print("Elige una opción: ");
            opcion = sc.nextInt();

            switch (opcion) {

                case 1:
                    System.out.println("\n--- Libro 1 ---");
                    System.out.println(libro1);
                    System.out.println("\n--- Libro 2 ---");
                    System.out.println(libro2);
                    System.out.println("\n--- Libro 3 ---");
                    System.out.println(libro3);
                    System.out.println("\n--- Libro 4 ---");
                    System.out.println(libro4);
                    System.out.println("\n--- Libro 5 ---");
                    System.out.println(libro5);
                    System.out.println("\n--- Libro 6 ---");
                    System.out.println(libro6);
                    break;

                case 2:
                    if (usuarioActual.librosPrestados >= 2) {
                        System.out.println("No puedes pedir más de 2 libros.");
                        break;
                    }

                    System.out.println("\n¿Qué libro quieres pedir prestado?");
                    System.out.println("1. " + libro1.getTitulo());
                    System.out.println("2. " + libro2.getTitulo());
                    System.out.println("3. " + libro3.getTitulo());
                    System.out.println("4. " + libro4.getTitulo());
                    System.out.println("5. " + libro5.getTitulo());
                    System.out.println("6. " + libro6.getTitulo());
                    System.out.print("Opción: ");
                    int p = sc.nextInt();

                    Libro libroP = null;
                    if (p == 1) libroP = libro1;
                    else if (p == 2) libroP = libro2;
                    else if (p == 3) libroP = libro3;
                    else if (p == 4) libroP = libro4;
                    else if (p == 5) libroP = libro5;
                    else if (p == 6) libroP = libro6;

                    if (libroP != null && libroP.prestar()) {
                        usuarioActual.librosPrestados++;
                        System.out.println("Préstamo realizado con éxito.");
                    } else {
                        System.out.println("No hay copias disponibles.");
                    }
                    break;

                case 3:
                    System.out.println("\n¿Qué libro quieres devolver?");
                    System.out.println("1. " + libro1.getTitulo());
                    System.out.println("2. " + libro2.getTitulo());
                    System.out.println("3. " + libro3.getTitulo());
                    System.out.println("4. " + libro4.getTitulo());
                    System.out.println("5. " + libro5.getTitulo());
                    System.out.println("6. " + libro6.getTitulo());
                    System.out.print("Opción: ");
                    int d = sc.nextInt();

                    Libro libroD = null;
                    if (d == 1) libroD = libro1;
                    else if (d == 2) libroD = libro2;
                    else if (d == 3) libroD = libro3;
                    else if (d == 4) libroD = libro4;
                    else if (d == 5) libroD = libro5;
                    else if (d == 6) libroD = libro6;

                    if (libroD != null && libroD.devolver()) {
                        usuarioActual.librosPrestados--;
                        System.out.println("Devolución completada.");
                    } else {
                        System.out.println("No tienes ese libro.");
                    }
                    break;

                case 4:
                    System.out.println("Libros prestados por " + usuarioActual.nombre + ": "
                            + usuarioActual.librosPrestados);
                    break;

                case 5:
                    System.out.println("Saliendo de la biblioteca...");
                    break;

                default:
                    System.out.println("Opción no válida.");
            }

        } while (opcion != 5);

        sc.close();
    }
}

````
**Salida real**  
Tienes un usuario? (si/no): no
Quieres crear un usuario? (si/no): si
Creando nuevo usuario
Escribe tu nombre: Angel
Ingresa tu edad: 18
Elige un ID de 4 dígitos (ex. 1234): 1404
Usuario creado
Bienvenido Angel

=== MENÚ BIBLIOTECA ===
1. Ver información de los libros
2. Pedir prestado un libro
3. Devolver un libro
4. Ver cantidad de libros que tienes
5. Salir
Elige una opción: 1

--- Libro 1 ---
Título: El Señor de los Anillos
Autor: Tolkien
Género: Fantasía
Año: 1954
Copias totales: 3
Prestadas: 0
Disponibles: 3

--- Libro 2 ---
Título: Cien años de soledad
Autor: García Márquez
Género: Novela
Año: 1967
Copias totales: 2
Prestadas: 0
Disponibles: 2

--- Libro 3 ---
Título: La metamorfosis
Autor: Kafka
Género: Novela
Año: 1915
Copias totales: 4
Prestadas: 0
Disponibles: 4

--- Libro 4 ---
Título: La odisea
Autor: Homero
Género: Epopeya
Año: 700
Copias totales: 2
Prestadas: 0
Disponibles: 2

--- Libro 5 ---
Título: Estravagario
Autor: Pablo Neruda
Género: Poesía
Año: 1958
Copias totales: 3
Prestadas: 0
Disponibles: 3

--- Libro 6 ---
Título: Danza de Dragones
Autor: George R. R. Martin
Género: Fantasía
Año: 2011
Copias totales: 2
Prestadas: 0
Disponibles: 2

=== MENÚ BIBLIOTECA ===
1. Ver información de los libros
2. Pedir prestado un libro
3. Devolver un libro
4. Ver cantidad de libros que tienes
5. Salir
Elige una opción: 2

¿Qué libro quieres pedir prestado?
1. El Señor de los Anillos
2. Cien años de soledad
3. La metamorfosis
4. La odisea
5. Estravagario
6. Danza de Dragones
Opción: 1
Préstamo realizado con éxito.

=== MENÚ BIBLIOTECA ===
1. Ver información de los libros
2. Pedir prestado un libro
3. Devolver un libro
4. Ver cantidad de libros que tienes
5. Salir
Elige una opción: 2

¿Qué libro quieres pedir prestado?
1. El Señor de los Anillos
2. Cien años de soledad
3. La metamorfosis
4. La odisea
5. Estravagario
6. Danza de Dragones
Opción: 4
Préstamo realizado con éxito.

=== MENÚ BIBLIOTECA ===
1. Ver información de los libros
2. Pedir prestado un libro
3. Devolver un libro
4. Ver cantidad de libros que tienes
5. Salir
Elige una opción: 2
No puedes pedir más de 2 libros.

=== MENÚ BIBLIOTECA ===
1. Ver información de los libros
2. Pedir prestado un libro
3. Devolver un libro
4. Ver cantidad de libros que tienes
5. Salir
Elige una opción: 4
Libros prestados por Angel: 2

=== MENÚ BIBLIOTECA ===
1. Ver información de los libros
2. Pedir prestado un libro
3. Devolver un libro
4. Ver cantidad de libros que tienes
5. Salir
Elige una opción: 3

¿Qué libro quieres devolver?
1. El Señor de los Anillos
2. Cien años de soledad
3. La metamorfosis
4. La odisea
5. Estravagario
6. Danza de Dragones
Opción: 4
Devolución completada.

=== MENÚ BIBLIOTECA ===
1. Ver información de los libros
2. Pedir prestado un libro
3. Devolver un libro
4. Ver cantidad de libros que tienes
5. Salir
Elige una opción: 5
Saliendo de la biblioteca...
