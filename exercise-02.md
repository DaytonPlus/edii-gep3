![[navbar]]
## Ejercicio 2
En determinado sitio se tiene una enorme red de computadoras interconectadas. Esta red contiene información sensible de la organización, por lo que debe ser protegida contra todo tipo de ataques o contaminación por virus. En la estrategia de protección, se analizan primero las estaciones más vulnerables y luego las menos vulnerables. Teniendo en cuenta el diagrama de clases descrito a continuación.

| RedComputadoras                                                                                                                                                                                                           |
| :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| # conexiones: lógico `[][]`<br># computadoras: `Lista<Computadora>`                                                                                                                                                       |
| + RedComputadoras()<br>+ HayMenosVulnerables(): lógico<br>+ cuantasAltamenteVulnerable(composibles: <br>`Lista<Computadora>`): entero<br>+ cuantosDiasTarda(computadora1: Computadora, computadora2: Computadora): entero |

| Computadora                                                                           |
| :------------------------------------------------------------------------------------ |
| # id: entero<br># ip: cadena<br># ubicacion: cadena                                   |
| + Computadora()<br>+ getID(): entero<br>+ getIP(): cadena<br>+ getUbicacion(): cadena |
a) Implemente el método HayMenosVulnerables(): lógico que permite determinar si hay al menos una computadora de baja vulnerabilidad, es decir, que no se comunica con ninguna otra computadora, por lo que ante un ataque no sería afectada.

b) Implemente el método cuantasAltamenteVulnerable(composibles: `Lista<Computadora>`): entero, el cual retorna el número de computadoras altamente vulnerables de la lista pasada por parámetro. Una computadora es altamente vulnerable cuando tiene conexión con más de 4 computadoras.

c) Se desea saber cuántos días tarda en infectarse con un virus X la computadora 2 luego de que se infecte la computadora 1. Cuando una computadora se infecta con el virus X, al día siguiente se propaga a todas las computadoras conectadas directamente a ella, ese proceso de propagación del virus continúa hasta que todas las computadoras a las que puede alcanzar estén infectadas. Implemente el método cuantosDiasTarda( computadora1: Computadora, computadora2: Computadora): entero, que devuelve la cantidad de días que demora en ser infectada la computadora 2 luego de que la computadora 1 fue infectada. Si no existiera comunicación entre estas dos computadoras se debe retornar -1.


###### Respuestas
```java
public List<Computadora> AdyacentesA(Computadora c) {
  List<Computadora> adys = new LinkedList<>();
  int pos = computadoras.indexOf(c);
  if(c == -1) return adys;
  
  boolean conex = conexiones[pos];

  for(int i=0;i<conex.length;i++) {
    if(conex[i]) adys.add(computadoras.get(i));
  }
  
  return adys;
}
```

```java
// Respuesta a)
public boolean HayMenosVulnerables() {
  for(Computadora c : computadoras) {
    if(AdyacentesA(c)==0) return true;
  }
  return false;
}
```

```java
// Respuesta b)
public int cuantasAltamenteVulnerable(Lista<Computadora> composibles) {
  int cant = 0;
  for(Computadora c : composibles) {
    if(AdyacentesA(c)>4) cant++;
  }
  return cant;
}
```

```java
// Respuesta c)
public int cuantosDiasTarda(Computadora c1, Computadora c2) {
  int[] nivel = new int[computadoras.size()];
  List<Computadora> visitadas = new LinkedList<>();

  Queue<Computadora> cola = new Queue<>();
  cola.offer(c1);
  nivel[computadoras.indexOf(c1)] = 0;
  
  while(!cola.empty()) {
    Computadora c = cola.poll();
    visitadas.add(c);
    int n = nivel[computadoras.indexOf(c)]

    for(Computadora a : AdyacentesA(c)) {
      if(!visitadas.contains(a)) {
        nivel[computadoras.indexOf(a)] = n+1;
        cola.offer(a);
        visitadas.add(a);
      }
    }
  }

  int n = nivel[computadoras.indexOf(c2)];
  if(n==0) return -1;
  return n;
}

```

