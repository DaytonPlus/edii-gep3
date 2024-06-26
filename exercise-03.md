#### Ejercicios
* [#1 - Red Social | Persona](exercise-01.md)
* [#2 - RedComputadoras | Computadora](exercise-02.md)
* [#3 - Pueblo](exercise-03.md)
* [#4 - Europa | Pais](exercise-04.md)
* [#5 - Red Electrica | Casas](exercise-05.md)
* [#6 - Hermandad | Jugador](exercise-06.md)
* [#7 - Laberinto | Sala](exercise-07.md)
* [#8 - Raid | Jugador](exercise-08.md)

## Ejercicio 3
La Comisión Internacional para la Prevención de Estafas está estudiando los posibles efectos de un esquema piramidal en un pueblo. El esquema es el siguiente: alguien le pide a otra persona $1, y le dice que les pida a otras dos personas $1 cada una y que, además, le diga a cada una que les pidan a otras dos personas dinero justo como ellos están haciendo. De esta forma, la víctima piensa que va a
ganar $1. Como hay un número finito de personas en el mundo, no todos pueden ganar dinero de esta manera, esto es una estafa.
Las N personas en el pueblo son susceptibles a la estafa, por lo que están dispuestas a dar $1 y luego pedir dinero a otras dos personas. Sin embargo, están dispuestas a participar solo una vez, lo que significa que, si les vuelven a preguntar, no darán dinero ni preguntarán a nadie. Una vez que a alguien se le pida dinero, esa persona lo dará y automáticamente les preguntará a dos más por dinero. 
Esto se podría representar como un grafo dirigido y no ponderado, donde cada vértice contiene el nombre de una persona del pueblo, y cada persona tiene dos, y solo dos, conexiones, las cuales serían las personas a quien le pedirá dinero.
Para ellos se cuenta con el siguiente diagrama de clases:

| Pueblo                                                                                                    |
| :-------------------------------------------------------------------------------------------------------- |
| personas: `Lista <cadena>`<br>conexiones: `logico [][]`                                                   |
| + Pueblo()<br>+ sePidenEntreSi(): lógico<br>+ personasQuePierden(nombreInicial: cadena): `Lista <cadena>` |

a) Implementa el método sePidenEntreSi(): lógico, que retorna verdadero si existe al menos un par de personas que se pidan dinero entre ellos, retorna falso en caso contrario.
```java
public boolean sePidenEntreSi() {
  for(int i=0;i<personas.size();i++) {
    for(int j=0;j<personas.size();j++) {
      if(sePiden(i, j)) return true;
    }
  }
  return false;
}

public boolean sePiden(int i, int j) {
  return conexiones[i][j] && conexiones[j][i];
}
```

b) Se quiere identificar quiénes del pueblo pierden dinero. Alguien pierde dinero cuando, no gana, ni repone, o sea, cuando pregunta por dinero a dos personas que ya están dentro de la estafa. Para ello implemente el método personasQuePierden(nombreInicial: cadena): `Lista <cadena>`, el cual recibe por parámetro el nombre de la 1ra persona que comienza la estafa y retorna una lista con los nombres de las personas que pierden dinero.
```java
public List<String> personasQuePierden(String nombreInicial) {
    List<String> lista = new LinkedList<>();
    List<String> visitadas = new LinkedList<>();
    Queue<String> cola = new Queue<>();
    
    cola.offer(nombreInicial);

    while (!cola.isEmpty()) {
        String nombre = cola.poll();
        visitadas.add(nombre);
        
        for (int i = 0; i < 2; i++) {
            String c = conexiones[personas.indexOf(nombre)][i];
            if (c != null) {
                if(!visitadas.contains(c)) cola.offer(c);
                else lista.add(c);
            }
        }
    }

    return lista;
}
```