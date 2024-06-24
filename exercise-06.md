#### Ejercicios
* [#1 - Red Social | Persona](exercise-01.md)
* [#2 - RedComputadoras | Computadora](exercise-02.md)
* [#3 - Pueblo](exercise-03.md)
* [#4 - Europa | Pais](exercise-04.md)
* [#5 - Red Electrica | Casas](exercise-05.md)
* [#6 - Hermandad | Jugador](exercise-06.md)
* [#7 - Laberinto | Sala](exercise-07.md)
* [#8 - Raid | Jugador](exercise-08.md)

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
```java
public boolean esFraternidad() {
  for(int i=0;i<jugadores.size();i++) {
    for(int j=i+1;j<jugadores.size();j++) {
      if(!sonAmigos(i, j)) return false;
    }
  }
  
  return true;
}

public boolean sonAmigos(int i, int j) {
  return amistad.get(i).contains(j) && amistad.get(j).contains(i);
}
```

b) Los jugadores cuentan con unos puntos de logro que indican que tanto han logrado hacer en el juego. Implemente el método compararLogros(j: Jugador): logico que devuelve verdadero solo si el jugador pasado por parámetros tiene más puntos de logro que todos y cada uno de sus amigos.
```java
public boolean compararLogros(Jugador j) {
  int pts = j.getPuntosLogro();
  
  for(Jugador a : amistad.get(j.getID())) {
    if(a.getPuntosLogro() > pts) return false;
  }
  
  return true;
}
```