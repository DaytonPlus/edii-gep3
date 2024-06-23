![[navbar]]
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

b) Se desea conocer, por propósitos de exploración, cuáles salas adyacentes se encuentran derrumbadas. Implemente el método salasDerrumbadas(salaActual: Sala): `Lista <Sala>` que, a partir de la sala actual pasada por parámetros, devuelva una lista con las salas derrumbadas a su alrededor.

##### Respuestas

```java
// Respuesta a)
public int salidaRapida(Sala origen) {

}
```

```java
// Respuesta a)
public List<Sala> salasDerrumbadas(Sala salaActual)  {

}
```