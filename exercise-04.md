![[navbar]]

## Ejercicio 4
Una empresa de envíos se encarga de entregas de paquetes por toda Europa, los cuales parten de un país y deben llegar a otro en la región. El siguiente diagrama de clases representa la región, contiene una lista de países y una matriz que contiene cuales países tienen fronteras terrestres con otros. De cada país se conoce su nombre y un valor de influencia que determina su importancia comercial para la empresa.

| Europa                                                                                             |
| :------------------------------------------------------------------------------------------------- |
| - paises: Lista `<Pais>`<br>- fronterasTerrestres: `logico[][]`                                    |
| + Europa()<br>+ altaImportancia(p: Pais): logico<br>+ entrega(origen: Pais, destino: Pais): logico |

| Pais                                                           |
| :------------------------------------------------------------- |
| # nombre: cadena<br># influencia: entero                       |
| + Pais()<br>+ getNombre(): cadena<br>+ getInfluencia(): entero |
a) Debe implementar el método altaImportancia(p: Pais): boolean que devuelve verdadero cuando un país tiene fronteras terrestres con más de 4 países o la importancia de 2 de los países con quienes colinda es mayor que 7.

b) La empresa no puede realizar envíos por vía marítima, por tanto, habrá países a los que no podrá llegar una determinada entrega. Implemente el método entrega(origen: Pais, destino: Pais): logico que devuelve verdadero si es posible llegar desde un país origen a uno destino por vía terrestre, y falso en caso contrario.

##### Respuestas

```java
// Respuesta a)
public boolean altaImportancia(Pais p) {

}
```

```java
// Respuesta b)
public boolean entrega(Pais origen, Pais destino) {

}
```