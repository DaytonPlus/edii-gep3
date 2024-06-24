#### Ejercicios
* [#1 - Red Social | Persona](exercise-01.md)
* [#2 - RedComputadoras | Computadora](exercise-02.md)
* [#3 - Pueblo](exercise-03.md)
* [#4 - Europa | Pais](exercise-04.md)
* [#5 - Red Electrica | Casas](exercise-05.md)
* [#6 - Hermandad | Jugador](exercise-06.md)
* [#7 - Laberinto | Sala](exercise-07.md)
* [#8 - Raid | Jugador](exercise-08.md)

## Ejercicio 7
Se desea hacer una simulación de exploración de un laberinto existente para que las incursiones en este sean más seguras. El Laberinto cuenta con salas y pasillos que las unen, en la clase se representan, mediante una matriz, las conexiones entre las salas. Algunas de estas salas se han derrumbado así que no se puede acceder a ellas.

| Laberinto                                                                                                     |
| :------------------------------------------------------------------------------------------------------------ |
| # salas: `Lista<Sala>`<br># conexiones: `logico[][]`                                                          |
| + Laberinto()<br>+ salidaRapida(origen: Sala): entero<br>+ salasDerrumbadas(salaActual: Sala): `Lista <Sala>` |

| Sala                                                                                |
| :---------------------------------------------------------------------------------- |
| # id: entero<br># derrumbada: logico<br># salida: logico                            |
| + Sala()<br>+ getID(): entero<br>+ getDerrumbada(): logico<br>+ getSalida(): logico |

a) Debe implementar el método salidaRapida(origen: Sala): entero que recibe por parámetro la sala desde donde se comienza y tiene que devolver la longitud del camino más corto desde esa sala hasta la salida. Solo una de las salas del laberinto es la salida.
```java
public int salidaRapida(Sala origen) {
  int[] distancias = new int[salas.size()];
  List<Sala> visitadas = new LinkedList<>();
  Queue<Sala> cola = new LinkedList<>();

  cola.offer(origen);
  distancias[origen.getID()] = 0;
  
  while(!cola.empty()) {
    Sala s = cola.poll();
    visitadas.add(s);

    int d = distancias[s.getID()];

    if(s.getDerrumbada()) continue;
    if(s.getSalida()) return d;
    
    for(Sala a : AdyacentesA(s)) {
      if(!visitadas.contains(a)) {
        cola.offer(a);
        distancias[a.getID()] = d + 1;
      }
    }
  }
  
  return -1;
}

public List<Sala> AdyacentesA(Sala s) {
  List<Sala> lista = new LinkedList<>();
  
  int pos = salas.indexOf(s);

  if(pos != -1) {
    for(int i=0;i<conexiones[pos].length;i++) {
      if(conexiones[pos][i]) lista.add(salas.get(i));
    }
  }
  
  return adys;
}
```


b) Se desea conocer, por propósitos de exploración, cuáles salas adyacentes se encuentran derrumbadas. Implemente el método salasDerrumbadas(salaActual: Sala): `Lista <Sala>` que, a partir de la sala actual pasada por parámetros, devuelva una lista con las salas derrumbadas a su alrededor.
```java
public List<Sala> salasDerrumbadas(Sala salaActual)  {
  List<Sala> lista = new LinkedList<>();
  List<Sala> visitadas = new LinkedList<>();
  Queue<Sala> cola = new LinkedList<>();

  cola.offer(origen);
  
  while(!cola.empty()) {
    Sala s = cola.poll();
    visitadas.add(s);

    if(s.getDerrumbada()) {
      lista.add(s);
      continue;
    }
    
    for(Sala a : AdyacentesA(s)) {
      if(!visitadas.contains(a)) {
        cola.offer(a);
      }
    }
  }
  
  return lista;
}
```