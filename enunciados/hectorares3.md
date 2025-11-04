# Examen Parcial - hectorares3

**Usuario GitHub:** hectorares3
**Fecha:** 4 de noviembre de 2025
**Retos tenidos en cuenta:** Reto 003

---

## Instrucciones

A continuación encontrarás fragmentos de código extraídos de tus entregas. Cada fragmento contiene una o más situaciones relacionadas con los conceptos vistos en clase.

Para cada pregunta debes:
1) Identificar a qué se refiere la observación
2) Explicar si es o no un error y por qué
3) Proponer la corrección

Nota: Responde 5 de las 8 preguntas (en función a lo indicado en el examen).


---

## Pregunta 1

Archivo: `Hotel.java` — [Ver archivo](https://github.com/mmasias/25-26-PRG1/blob/54b37c9b9f12ac5776649e3dd1cd8aa14198a8de/entregas/aresHector/Hotel.java) (Reto 003)

```java
class SimulacionHotel {
    // ...
}
```

¿Qué observas en este código?

En este código observo que, en efecto, hay un error claro de despiste en el que la clase no se ha nombrado adecuadamente ya que el nombre de la clase debe coincidir con el del archivo. La solución para este error sería cambiar o bien el nombre de la clase o bien el del archivo.java para que todo quede en orden y en correcto funcionamiento. En java, el nombre del fichero y el de la clase pública debén coincidir.

---

## Pregunta 2

Archivo: `Hotel.java` — [Ver archivo](https://github.com/mmasias/25-26-PRG1/blob/54b37c9b9f12ac5776649e3dd1cd8aa14198a8de/entregas/aresHector/Hotel.java) (Reto 003)

```java
if (!hayRayo && random.nextDouble() < PROB_RAYO) {
    hayRayo = true;
    columnaRayo = 1 + random.nextInt(HABITACIONES);
}
```

¿Qué observas en este código?

En este fragmento, ocurre un problema y es que solo lo he inicializado a false una vez al inicio del bucle de día. Esto conlleva que si la probabilidad de que haya un rayo se cumple, se cambia a true y permance así ya que la variable nunca se llega a "resetear". Por lo tanto si cae un rayo al inicio del día, la columna permanece inutlizada para el resto del desarrollo de la simulación. Por lo tanto, se debería buscar la forma de que este probabilidad se repitiera de forma continúa para que no sea un evento aleatorio que solo pueda suceder una vez en la simulación. 

Para simular un evento que puede ocurrir aleatoriamente cada hora, las variables hayRayo y columnaRayo deben ser declaradas al comienzo de cada ciclo de la hora.

```java
for (int hora = 0; hora < HORAS; hora++) {
    
    boolean hayRayo = false;
    int columnaRayo = -1;

    if (random.nextDouble() < PROB_RAYO) {
        hayRayo = true;
        columnaRayo = 1 + random.nextInt(HABITACIONES);
    }
}
```


---

## Pregunta 3

Archivo: `Hotel.java` — [Ver archivo](https://github.com/mmasias/25-26-PRG1/blob/54b37c9b9f12ac5776649e3dd1cd8aa14198a8de/entregas/aresHector/Hotel.java) (Reto 003)

```java
boolean persianaAbierta = random.nextDouble() < PROB_PERSIANA;
boolean luzEncendida = random.nextDouble() < PROB_LUZ;
if (persianaAbierta && luzEncendida) {
    celda = SIMBOLO_PERSIANA_LUZ;
} else if (persianaAbierta) {
    celda = SIMBOLO_PERSIANA;
} else {
    celda = SIMBOLO_VACIO;
}
```

¿Qué observas en este código?

---

## Pregunta 4

Archivo: `Hotel.java` — [Ver archivo](https://github.com/mmasias/25-26-PRG1/blob/54b37c9b9f12ac5776649e3dd1cd8aa14198a8de/entregas/aresHector/Hotel.java) (Reto 003)

```java
if (SIMBOLO_PERSIANA_LUZ.equals(celda)) {
    consumoHora++;
}
System.out.print(celda + ":");
```

¿Qué observas en este código?

En este fragmento observo un error que va a repercutir directamente en el consumo del edificio ya que solo he tenido en cuenta el consumo por hora cuando la persiana esta bajada pero la luz sigue encendida. Entonces, cuando eso ocurre, el if de consumo nunca se llega a cumplir ya que la celda queda con un SIMBOLO_VACIO por lo tanto se ignora el consumo de la luz en ese momento.
Se debe modificar la lógica del programa para que cuando la persiana este abajo pero la luz este encendida siga contando el consumo de dicha luz

```java

String celda;
if (hayRayo && columna == columnaRayo) {
    celda = SIMBOLO_RAYO;
} else if (hayMantenimiento && planta == plantaMantenimiento && hora >= horaMantenimiento) {
    celda = SIMBOLO_MANTENIMIENTO;
} else {
    boolean persianaAbierta = random.nextDouble() < PROB_PERSIANA;
    boolean luzEncendida = random.nextDouble() < PROB_LUZ;
    
    
    if (persianaAbierta && luzEncendida) {
        celda = SIMBOLO_PERSIANA_LUZ;
    } else if (persianaAbierta) {
        celda = SIMBOLO_PERSIANA;
    } else if (luzEncendida) {
        celda = SIMBOLO_PERSIANA_LUZ;
    } else {
        celda = SIMBOLO_VACIO;
    }

    if (luzEncendida) {
        consumoHora++;
    }
}
System.out.print(celda + ":");

```
De esta manera saldrían los símbolos correctamente además de tener en cuenta el consumo de luz independientemente de que la persiana se encuentre cerrada

---

## Pregunta 5

Archivo: `Hotel.java` — [Ver archivo](https://github.com/mmasias/25-26-PRG1/blob/54b37c9b9f12ac5776649e3dd1cd8aa14198a8de/entregas/aresHector/Hotel.java) (Reto 003)

```java
double mediaSemanal = consumoTotalSemana / (double) DIAS;
System.out.printf("Media semanal: %.2f%n", mediaSemanal);
```

¿Qué observas en este código?
En este fragmento de código puedo entender que hay dos cosas a mejorar, la primera es una cuestión de limpieza y orden del código ya que no es correcto usar println durante todo el código para a continuación usar printf para imprimir una línea ya que se debería usar el mismo formato a lo largo de todo el código por cuestiones de limpieza.

Además, pienso que se podría implementar una validación para comprobar que el día sea mayor que 0 y no obtener una división entre 0

```java
double mediaSemanal = 0;
if (DIAS > 0) {
    mediaSemanal = consumoTotalSemana / (double) DIAS;
}
System.out.printf("Media semanal: %.2f%n", mediaSemanal);
```

---

## Pregunta 6

Archivo: `Hotel.java` — [Ver archivo](https://github.com/mmasias/25-26-PRG1/blob/54b37c9b9f12ac5776649e3dd1cd8aa14198a8de/entregas/aresHector/Hotel.java) (Reto 003)

```java
class SimulacionHotel {

    private static final int PLANTAS = 7;
    private static final int HABITACIONES = 6;
```

¿Qué observas en este código?

---

## Pregunta 7

Archivo: `Hotel.java` — [Ver archivo](https://github.com/mmasias/25-26-PRG1/blob/54b37c9b9f12ac5776649e3dd1cd8aa14198a8de/entregas/aresHector/Hotel.java) (Reto 003)

```java
if (hayRayo && columna == columnaRayo) {
    celda = SIMBOLO_RAYO;
} else if (hayMantenimiento && planta == plantaMantenimiento && hora >= horaMantenimiento) {
    celda = SIMBOLO_MANTENIMIENTO;
} else {
    boolean persianaAbierta = random.nextDouble() < PROB_PERSIANA;
    boolean luzEncendida = random.nextDouble() < PROB_LUZ;
    if (persianaAbierta && luzEncendida) {
        celda = SIMBOLO_PERSIANA_LUZ;
    } else if (persianaAbierta) {
        celda = SIMBOLO_PERSIANA;
    } else {
        celda = SIMBOLO_VACIO;
    }
}
```

¿Qué observas en este código?

---

## Pregunta 8

Archivo: `Hotel.java` — [Ver archivo](https://github.com/mmasias/25-26-PRG1/blob/54b37c9b9f12ac5776649e3dd1cd8aa14198a8de/entregas/aresHector/Hotel.java) (Reto 003)

```java
if (hayRayo)
    System.out.println("Un rayo ha inutilizado la columna " + columnaRayo);
if (hayMantenimiento && hora == horaMantenimiento)
    System.out.println(plantaMantenimiento + "ª planta en mantenimiento");
```

¿Qué observas en este código?

En este fragmento observo que le faltan las llaves al condicional if.
Aunque el código funcione, no está bien hecho y puede conducir a errores de lógica por lo que debo añadirle las llaves correspondientes

```java

if (hayRayo) {
    System.out.println("Un rayo ha inutilizado la columna " + columnaRayo);
}
if (hayMantenimiento && hora == horaMantenimiento) {
    System.out.println(plantaMantenimiento + "ª planta en mantenimiento");
}
```
