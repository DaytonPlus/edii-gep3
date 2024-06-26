#### Ejercicios
* [#1 - Red Social | Persona](exercise-01.md)
* [#2 - RedComputadoras | Computadora](exercise-02.md)
* [#3 - Pueblo](exercise-03.md)
* [#4 - Europa | Pais](exercise-04.md)
* [#5 - Red Electrica | Casas](exercise-05.md)
* [#6 - Hermandad | Jugador](exercise-06.md)
* [#7 - Laberinto | Sala](exercise-07.md)
* [#8 - Raid | Jugador](exercise-08.md)

## Ejercicio 5
La red eléctrica de una ciudad está organizada por diferentes circuitos, cada uno de estos circuitos está formado por un grupo de casas cuya red eléctrica está conectada entre sí. Los circuitos permanecen prácticamente aislados entre sí de manera que si ocurre un problema eléctrico en uno de los circuitos solo se afecte el servicio de ese circuito. El siguiente diagrama de clases contiene una lista con todas las casas en la ciudad y una matriz que representa las conexiones eléctricas entre ellas:

| RedElectrica                                                                                                                    |
| :------------------------------------------------------------------------------------------------------------------------------ |
| # casas: `Lista<Casa>`<br># conexiones: `logico[][]`                                                                            |
| + RedElectrica()<br>+ casasInterconectadas(casa1: Casa, casa2: <br>Casa): boolean<br>+ casasEnRiesgo(casa: Casa): `Lista<Casa>` |

| Casa                                                              |
| :---------------------------------------------------------------- |
| # numero: entero<br># cortoCircuito: logico                       |
| + Casa()<br>+ getNumero(): entero<br>+ getCortoCircuito(): logico |

a) Implemente el método casasInterconectadas(casa1: Casa, casa2: Casa): boolean que, recibiendo dos casas por párametro, devuelva verdadero si ambas casas están en el mismo circuito.
```java
public boolean casasInterconectadas(Casa c1, Casa c2) {
  List<Casa> visitadas = new LinkedList<>();
  BPP(c1, visitadas);
  return visitadas.contains(c2);
}

public BPP(Casa c, List<Casa> visitadas) {
  visitadas.add(c);
  
  for(Casa a : AdyacentesA(c)) {
    if(!visitadas.contains(a)) BPP(a, visitadas);
  }
}

public List<Pais> AdyacentesA(Casa c) {
  List<Pais> adys = new LinkedList<>();
  
  int pos = casas.indexOf(c);
  
  if(pos != -1) {
    for(int i=0;i<conexiones[pos].length;i++) {
      if(conexiones[pos][i]) {
        adys.add(casas.get(i));
      }
    }
  }
  
  return adys;
}
```

b) Cuando una casa tiene un cortocircuito en su red interna es posible que tenga consecuencias negativas para las casas directamente conectadas a ella. Implemente el método casasEnRiesgo(casa: Casa): `Lista<Casa>` el cual a partir de una casa devuelva las adyacentes que puedan estar en riego.
```java
public Lista<Casa> casasEnRiesgo(Casa casa) {
  List<Casa> lista = new LinkedList<>();
  List<Casa> visitadas = new LinkedList<>();
  Queue<Casa> cola = new Queue<>();
  
  cola.offer(casa);
  
  while(!cola.empty()) {
    Casa c = cola.poll();
    visitadas.add(c);

    boolean enRiesgo = c.getCortoCircuito();

    for(Persona a : AdyacentesA(c)) {
      if(!visitadas.contains(a)) {
        if(enRiesgo || a.getCortoCircuito()) {
          cola.offer(a);
          lista.add(a);
        }
      }
    }
  }
  
  return lista;
}
```