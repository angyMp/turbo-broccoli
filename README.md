package listasimple;

public class Nodo {
    String name; // Campo de datos
    Nodo next;   // Campo enlace
}

package listasimple;

public class ListaSimple {
    Nodo top;

    // Métodos para los casos de inserción de nodos
    public boolean insertaPrimerNodo(String dato) {
        if (top == null) { // La lista está vacía
            top = new Nodo();
            top.name = dato;
            top.next = null;
            return true;
        } else {
            return false;
        }
    }

    public void insertaAntesPrimerNodo(String nombre) {
        Nodo temp;
        temp = new Nodo();
        temp.name = nombre;
        temp.next = this.top;
        this.top = temp;
        temp = null;
    }

    public void insertaAlFinal(String nombre) {
        Nodo temp = new Nodo();
        temp.name = nombre;
        temp.next = null;
        Nodo temp2 = this.top;

        while (temp2.next != null)
            temp2 = temp2.next;

        temp2.next = temp;
        temp = null;
    }

//    public boolean insertaEntreNodos(String nombre, String buscado) {
//        Nodo temp = new Nodo();
//        temp.name = nombre;
//        Nodo temp2 = this.top;
//
//        while ((temp2 != null) && !temp2.name.equals(buscado)) {
//            temp2 = temp2.next;
//        }
//
//        if (temp2 != null) { // Nodo buscado se encontró
//            temp.next = temp2.next;
//            temp2.next = temp;
//            temp = null;
//            return true;
//        } else {
//            return false;
//        }
//    }

    public void imprimir() {
         System.out.println("Contenido: ");
        for (Nodo temp = this.top; temp != null; temp = temp.next) {             
             System.out.print("[ " + temp.name + " ] -> ");
        }         
        System.out.print("[...]\n");
    }

//    public String String() {
//        StringBuilder cadAux = new StringBuilder();
//        for (Nodo temp = this.top; temp != null; temp = temp.next) {
//            cadAux.append("[ ").append(temp.name).append(" ] -> ");
//        }
//
//        cadAux.append("[X]\n");
//
//        return cadAux.toString();
//    }

    // Métodos de borrado
    public void borrarPrimerNodo() {
        this.top = this.top.next;
    }

    // Borrar cualquier nodo que no sea el primero
    public boolean borrarCualquierNodo(String buscado) {
        Nodo temp = this.top;

        while ((temp != null) && !temp.name.equals(buscado)) {
            temp = temp.next;
        }

        if (temp != null) { // Nodo buscado se encontró
            temp.next = temp.next.next;
            temp = null;
            return true;
        } else {
            return false;
        }
    }
    /////////////////////////////////////////////////////////////////7
     // Métodos de búsqueda
    public Nodo buscarPorPosicion(int posicion) {
        int contador = 0;
        Nodo temp = this.top;

        while (temp != null) {
            if (contador == posicion) {
                return temp;
            }

            temp = temp.next;
            contador++;
        }

        return null; // Si la posición no existe en la lista
    }

    // Método para imprimir la lista indicando las posiciones
    public void imprimirConPosiciones() {
        Nodo temp = this.top;
        int posicion = 0;

        while (temp != null) {
            System.out.print("[ Posición " + posicion + ": " + temp.name + " ] -> ");
            temp = temp.next;
            posicion++;
        }

        System.out.print("[?]\n");
    }
    
    public boolean insertaAntesUltimoNodo(String nombre) {
        Nodo temp = new Nodo();
        temp.name = nombre;
        temp.next = null;

        // Caso especial: si la lista está vacía, inserta al principio
        if (top == null) {
            top = temp;
            return true;
        }

        // Caso general: recorre la lista hasta el penúltimo nodo
        Nodo temp2 = this.top;
        while (temp2.next != null && temp2.next.next != null) {
            temp2 = temp2.next;
        }

        // Inserta el nuevo nodo antes del último
        temp.next = temp2.next;
        temp2.next = temp;
        return true;
    }
    
    // Método para intercambiar un nodo por otro buscado
    public void intercambiarNodo(String nodoBuscado, String nuevoDato) {
        Nodo temp = this.top;

        while (temp != null && !temp.name.equals(nodoBuscado)) {
            temp = temp.next;
        }

        if (temp != null) {
            temp.name = nuevoDato;
            System.out.println("Nodo intercambiado exitosamente.");
        } else {
            System.out.println("Nodo no encontrado. No se realizó el intercambio.");
        }
    }
}



package listasimple;
import java.util.Scanner;

public class UsoListaSimple {
    public static void main(String[] args) {
        ListaSimple lista = new ListaSimple();

        lista.insertaPrimerNodo("A");
        lista.insertaAntesPrimerNodo("B");
        lista.insertaAlFinal("C");
       // lista.insertaEntreNodos("B", "A");
       System.out.println("Contenido al principio:");
       lista.imprimir();
       //System.out.print(lista);

        // Instanciar y ejecutar el menú
        MenuExample menu = new MenuExample(lista);
        menu.ejecutarMenu();
    }
}

class MenuExample {
    Scanner scanner = new Scanner(System.in);
    char opcion;
    ListaSimple lista;

    // Constructor que recibe la referencia de la lista
    public MenuExample(ListaSimple lista) {
        this.lista = lista;
    }

    public void ejecutarMenu() {
        do {
            System.out.println("---------------------------------------------------------");
            System.out.println("a. Buscar un nodo por su posición.");
            System.out.println("b. Insertar un nuevo nodo antes del último");
            System.out.println("c. Intercambiar un nodo por otro buscado");
            System.out.println("d. Salir");
            System.out.println("Seleccione una opción:");
            
            try {
                opcion = scanner.next().charAt(0);
            } catch (Exception e) {
                System.out.println("Error al leer la opción. Intente de nuevo.");
                scanner.nextLine(); // Limpiar el buffer del scanner
                continue; // Volver al inicio del bucle
            }
            
            
            switch (opcion) {
                case 'a':
                    System.out.println("---------------------------------------------------------");
                    lista.imprimirConPosiciones();

                    int posicionBuscada = 2; // Cambiar la posición 
                    Nodo nodoEncontrado = lista.buscarPorPosicion(posicionBuscada);

                    if (nodoEncontrado != null) {
                        System.out.println("Nodo encontrado en la posición " + posicionBuscada + ": " + nodoEncontrado.name);
                    } else {
                        System.out.println("No se encontró ningún nodo en la posición " + posicionBuscada);
                    }
                    break;
                    
                    
                case 'b':
                    
                    System.out.println("Ingrese el valor para el nuevo nodo (New)");                   
                    lista.insertaAntesUltimoNodo("New");
                    lista.imprimir();
                    
                    break;
                    
                    
                case 'c':
                    System.out.println("-Utilice el contenido del nodo que desea intercambiar-");
                    System.out.print("Ingrese el nodo que desea intercambiar: ");
                    String nodoBuscado = scanner.next();

                    System.out.print("Ingrese el nuevo valor para el nodo: ");
                    String nuevoDato = scanner.next();

                    lista.intercambiarNodo(nodoBuscado, nuevoDato);

                    System.out.println("Lista después del intercambio:");
                    lista.imprimir();

                   //scanner.close();
                    break;
                    
                    
                case 'D':
                    System.out.println("Saliendo del programa.");
                    break;
                default:
                    System.out.println("Opción no válida. Intente de nuevo.");
                    break;
            }

        } while (opcion != 'd');

        scanner.close();
    }
}

