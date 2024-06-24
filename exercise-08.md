#### Ejercicios
* [#1 - Red Social | Persona](exercise-01.md)
* [#2 - RedComputadoras | Computadora](exercise-02.md)
* [#3 - Pueblo](exercise-03.md)
* [#4 - Europa | Pais](exercise-04.md)
* [#5 - Red Electrica | Casas](exercise-05.md)
* [#6 - Hermandad | Jugador](exercise-06.md)
* [#7 - Laberinto | Sala](exercise-07.md)
* [#8 - Raid | Jugador](exercise-08.md)

## Ejercicio 8
Los sacerdotes siempre han sido famosos por sus útiles magias curativas que ayudan a mantener vivos a sus compañeros. Uno de los hechizos más importantes que tienen es Alivio, el cual es lanzado a un Jugador, lo sana en una cantidad igual al 20% de su vida máxima y luego salta al siguiente, pero no puede saltar a jugadores que se encuentran separados por más de 5 metros. La clase Raid contiene una lista con los jugadores en el grupo, así como una matriz con las distancias que separan a uno del otro. Esto se ve representado en los siguientes diagramas de clase:

| Raid                                                                                                                               |
| :--------------------------------------------------------------------------------------------------------------------------------- |
| # jugadores: `Lista <Jugador>`<br># distancias: `entero [][]`                                                                      |
| + Raid()<br>+ circuloSanacion(sacerdote: Jugador): `Lista <Jugador>`<br>+ castAlivio(jugador1: Jugador, jugador2: Jugador): logico |

| Jugador                                                     |
| :---------------------------------------------------------- |
| # nombre: cadena<br># vida: entero                          |
| + Jugador()<br>+ getNombre(): cadena<br>+ getVida(): entero |

a) Implemente el método castAlivio(jugador1: Jugador, jugador2 Jugador): logico que devuelve verdadero si es posible, teniendo a jugador1 como objetivo inicial, que Alivio llegue a sanar a jugador2.
```java
public boolean castAlivio(Jugador j1, Jugador j2) {
  List<Sala> visitadas = new LinkedList<>();
  Queue<Sala> cola = new LinkedList<>();

  cola.offer(j1);
  
  while(!cola.empty()) {
    Jugador j = cola.poll();
    visitadas.add(j);

    if(j == j2) return true;

    for(Jugador a : AdyacentesA(j)) {
      if(!visitadas.contains(a) && distancias[jugadores.indexOf(j)][jugadores.indexOf(a)] <= 5) {
        cola.offer(a);
      }
    }
  }
  
  return false;
}

public List<Jugador> AdyacentesA(Jugador j) {
  List<Jugador> lista = new LinkedList<>();
  
  int pos = jugadores.indexOf(j);
  
  if(pos != -1) {
    for(int i=0;i<distancias[pos].length;i++) {
      if(distancias[pos][i]) lista.add(jugadores.get(i));
    }
  }
  
  return adys;
}
```

b) Los sacerdotes tienen además un hechizo llamado Círculo de Sanación, es muy potente pero solo es capaz de curar a los jugadores a 8 metros alrededor del sacerdote que lo lanzó. Implemente el método circuloSanacion(sacerdote: Jugador): `Lista <Jugador>` que recibiendo un jugador por parámetros (el sacerdote que lanza el hechizo) devuelva una lista de jugadores a los que curó.
```java
public List<Jugador> circuloSanacion(Jugador sacerdote) {
    List<Jugador> curados = new LinkedList<>();
    List<Jugador> visitados = new LinkedList<>();
    Queue<Jugador> cola = new Queue<>();
    
    cola.offer(sacerdote);

    while (!cola.isEmpty()) {
        Jugador j = cola.poll();

        visitados.add(j);
        curados.add(j);

        for (Jugador a : jugadores) {
            if (!visitados.contains(a) && distancias[jugadores.indexOf(sacerdote)][jugadores.indexOf(a)] <= 8) {
                cola.offer(a);
            }
        }
    }

    return curados;
}
```

