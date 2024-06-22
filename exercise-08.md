
![[navbar]]
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

b) Los sacerdotes tienen además un hechizo llamado Círculo de Sanación, es muy potente pero solo es capaz de curar a los jugadores a 8 metros alrededor del sacerdote que lo lanzó. Implemente el método circuloSanacion(sacerdote: Jugador): `Lista <Jugador>` que recibiendo un jugador por parámetros (el sacerdote que lanza el hechizo) devuelva una lista de jugadores a los que curó.

##### Respuestas

```java
// Respuesta a)
public boolean castAlivio(Jugador j1, Jugador j2) {

}
```

```java
// Respuesta a)
public List<Jugador> circuloSanacion(Jugador sacerdote) {

}
