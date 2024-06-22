![[navbar]]
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

b) Cuando una casa tiene un cortocircuito en su red interna es posible que tenga consecuencias negativas para las casas directamente conectadas a ella. Implemente el método casasEnRiesgo(casa: Casa): `Lista<Casa>` el cual a partir de una casa devuelva las adyacentes que puedan estar en riego.

##### Respuestas

```java
// Respuesta a)
public boolean casasInterconectadas(Casa c1, Casa c2) {

}
```

```java
// Respuesta b)
public Lista<Casa> casasEnRiesgo(Casa casa) {

}
```