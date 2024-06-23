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
```java
public boolean HayMenosVulnerables() {
  for(Computadora c : computadoras) {
    if(esAislada(c)) return true;
  }
  
  return false;
}

public boolean esAislada(Computadora c) {
  return AdyacentesA(c).isEmpty();
}

public List<Computadora> AdyacentesA(Computadora c) {
  List<Computadora> adys = new LinkedList<>();
  int pos = c.getIndexOf(c);
  
  if(pos == -1) return adys;
  
  for(int i=0;i<conexiones[pos].length;i++) {
    if(conexiones[pos][i]) adys.add(computadoras.get(i));
  }
  
  return adys;
}
```

b) Implemente el método cuantasAltamenteVulnerable(composibles: `Lista<Computadora>`): entero, el cual retorna el número de computadoras altamente vulnerables de la lista pasada por parámetro. Una computadora es altamente vulnerable cuando tiene conexión con más de 4 computadoras.
```java
public int cuantasAltamenteVulnerable(Lista<Computadora> composibles) {
  int cant = 0;
  
  for(Computadora c : composibles) {
    if(AdyacentesA(c) > 4) cant++;
  }
  
  return cant;
}
```

c) Se desea saber cuántos días tarda en infectarse con un virus X la computadora 2 luego de que se infecte la computadora 1. Cuando una computadora se infecta con el virus X, al día siguiente se propaga a todas las computadoras conectadas directamente a ella, ese proceso de propagación del virus continúa hasta que todas las computadoras a las que puede alcanzar estén infectadas. Implemente el método cuantosDiasTarda( computadora1: Computadora, computadora2: Computadora): entero, que devuelve la cantidad de días que demora en ser infectada la computadora 2 luego de que la computadora 1 fue infectada. Si no existiera comunicación entre estas dos computadoras se debe retornar -1.
```java
public int cuantosDiasTarda(Computadora c1, Computadora c2) {
    boolean[] visitadas = new boolean[computadoras.size()];
    int[] dias = new int[computadoras.size()];
    
    Queue<Computadora> cola = new LinkedList<>();
    cola.offer(c1);
    visitadas[c1.getID()] = true;
    dias[c1.getID()] = 0;
    
    while (!cola.isEmpty()) {
        Computadora c = cola.poll();
        if (a.equals(c2)) ​return dias[a.getID()];
  
        for(Computadora a : AdyacentesA(c)) {
            if (!visitadas[a.getID()]) {
                visitadas[a.getID()] = true;
                dias[a.getID()] = dias[c.getID()] + 1;
                cola.offer(a);
            }
        }
    }
    
    return -1;
}

```

