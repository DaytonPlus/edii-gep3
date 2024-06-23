![[navbar]]
## Ejercicio 1
Se desea hacer un sistema para controlar el estado de una red social en internet. 
En dicha red social existe solo un tipo de relación, que es la relación de amistad. En 
la concepción del sistema se hizo el diseño de clases que se presenta a 
continuación. La clase RedSocial se modeló como un grafo no dirigido, donde los 
vértices son las personas y si dos personas son amigas entonces los nodos donde 
están almacenadas serían adyacentes. La estructura de datos utilizada es Lista de 
vértices – Matriz de adyacencia y se modela en el siguiente diagrama de clases.

|                           Persona                            |
| :----------------------------------------------------------- |
|             # nombre: cadena<br># email: cadena              |
| + Persona()<br>+ getNombre(): cadena<br>+ getEmail(): cadena |

| Red Social                                                                                                                                                                                                                                                                                                         |
| :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| # personas: `Lista<Persona>`<br># amistades: `lógico [][]`                                                                                                                                                                                                                                                         |
| + RedSocial()<br>+ amigosEnComun(p1: Persona, p2: Persona): Lista\<Persona\><br>+ amistadCompleta(amigos: `Lista<Persona>)`: lógico<br>+ cantPersonasConKAmigos(k: entero): entero<br>+ personasPopularesConexion(p1: Persona, p2: Persona): lógico<br>+ personasSinEnterarse(persona: Persona): `Lista<Personas>` |

a) Implemente el método amigosEnComun(p1: Persona, p2: Persona): `Lista<cadena>`, el cual recibe dos personas, p1 y p2, por parámetros y retorna la lista con los emails de las personas que son amigos de p1 y p2 al mismo tiempo.
```java
public Lista<String> amigosEnComun(Persona p1, Persona p2) {
  List<String> emails = new LinkedList<>();
  List<Persona> adys = AdyacentesA(p1);

  for(Persona p : AdyacentesA(p2)) {
    if(adys.contains(p)) emails.add(p.getEmail());
  }
  
  return emails;
}

public List<Persona> AdyacentesA(Persona p) {
  List<Persona> adys = new LinkedList<>();
  int pos = personas.indexOf(p);
  if(pos == -1) return adys;
  
  boolean amist = amistades[pos];

  for(int i=0;i<amist.length;i++) {
    if(amist[i]) adys.add(personas.get(i));
  }
  
  return adys;
}
```

b) Implemente el método amistadCompleta(amigos: `Lista<Persona>`): lógico, el cual determina si el conjunto de personas, representado por la lista pasada por parámetro, tienen amistad completa. Amistad completa se tiene si entre cualquier par de personas del grafo, existe una arista.
```java
public boolean amistadCompleta(Lista<Persona> amigos) {
  if(amigos.length == 0) return false;

  Persona p0 = amigos.get(0);
  List<Persona> adys = AdyacentesA(p0);

  for(Persona p : amigos) {
    if(p != p0 && !adys.contains(p)) return false;
  }
  
  return true;
}
```

c) Cada cierto tiempo en la red social se hacen análisis y estadísticas con respecto a la cantidad de amigos que tienen los usuarios. Implemente el método cantPersonasConKAmigos(k: entero): entero, el cual retorna la cantidad de personas en la red social que tengan tantos amigos como el número pasado por parámetro. 
```java
public int cantPersonasConKAmigos(entero k) {
  int cant = 0;
  
  for(Persona p : personas) {
    if(AdyacentesA(p).size() > k) cant++;
  }
  
  return cant;
}
```

d) Uno de los análisis que se realizan en la red social es ver si las personas populares, o sea, las que tengan más de 10 amigos, están conectadas. Implemente el método personasPopularesConexion(p1: Persona, p2: Persona): lógico, el cual devuelve verdadero en el caso de que las dos personas pasadas por parámetro tengan alguna conexión de amistades directa o indirectamente. Para realizar este procedimiento no se toman en cuenta las personas que no cumplan con las condiciones para ser populares.
```java
public boolean personasPopularesConexion(Persona p1, Persona p2) {
  if(!esPopular(p1) || !esPopular(p2)) return false;
  
  List<Persona> visitadas = new LinkedList<>();
  
  BPP(p1, visitadas);
  
  return visitadas.contains(p2);
}

public boolean esPopular(Persona p) {
  return AdyacentesA(p).size() > 10;
}

public void BPP(Persona p, List<Persona> viditadas) {
  visitadas.add(p);
  for(Persona a : AdyacentesA(p)) {
    if(!visitadas.contains(a)) BPP(a, visitadas);
  }
}
```

e) Cuando una persona publica alguna información importante, todos sus amigos la comparten a sus amigos directos para que estos la vean, a su vez, estos la vuelven a compartir, y así sucesivamente. Se puede intuir en el procedimiento anteriormente descrito que la divulgación de la información ocurre por niveles. Implemente el método personasSinEnterarse(persona: Persona): `Lista<Personas>`, el cual recibe por parámetro la persona que inicialmente hizo la publicación, y retorna la lista de personas que no podrán ver esa información si parte de ese usuario.
```java
public List<Persona> personasSinEnterarse(Persona p) {
  List<Persona> lista = new LinkedList<>();
  List<Persona> visitadas = new LinkedList<>();

  BPA(p, visitadas);

  for(Persona p1 : personas) {
    if(!visitadas.contains(p1)) lista.add(p1);
  }
  
  return lista;
}

public void BPA(Persona persona, List<Persona> visitadas) {
  Queue<Persona> cola = new Queue<>();
  cola.offer(persona);
  
  while(!cola.empty()) {
    Persona p = cola.poll();
    visitadas.add(p);
    
    for(Persona a : AdyacentesA(p)) {
      if(!visitadas.contains(a)) ​cola.offer(a);
    }
  }
}
```

