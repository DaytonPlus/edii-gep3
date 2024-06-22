![[navbar]]
## Ejercicio 6
En un juego en línea los jugadores pueden añadir a otros a su lista de amigos. Un jugador puede tener añadido a su lista de amigos a otro que a su vez no lo contemple a él en su lista de amigos, esto es lo que ven los jugadores, pero no es toda la información con la que trabaja el servidor. Para el servidor un jugador es amigo de otro si aparece en su lista de amigos o si analizando sucesivamente los amigos de los amigos el segundo jugador aparece como amigo de esos otros jugadores. Una Hermandad es un conjunto de jugadores que se unen para fines comunes, el servidor considera a una Hermandad como una Fraternidad si todos los miembros son amigos entre sí basado en las reglas del servidor.

| Hermandad                                                                          |
| :--------------------------------------------------------------------------------- |
| # jugadores: Lista `<Jugador>`<br># amistad: Lista `<Lista<Jugador>>`              |
| + Hermandad()<br>+ esFraternidad(): logico<br>+ compararLogros(j: Jugador): logico |

| Jugador                                                        |
| :------------------------------------------------------------- |
| # id: entero<br># puntosLogro: entero                          |
| + Jugador()<br>+ getID(): entero<br>+ getPuntosLogro(): entero |

a) Implemente el método esFraternidad(): logico que devuelve verdadero si la Hermandad es considerada una Fraternidad por parte del servidor y falso en caso contrario.

b) Los jugadores cuentan con unos puntos de logro que indican que tanto han logrado hacer en el juego. Implemente el método compararLogros(j: Jugador): logico que devuelve verdadero solo si el jugador pasado por parámetros tiene más puntos de logro que todos y cada uno de sus amigos.

###### Respuestas

```java
// Respuesta a)
public boolean esFraternidad() {

}
```

```java
// Respuesta b)
public boolean compararLogros(Jugador j) {

}
```