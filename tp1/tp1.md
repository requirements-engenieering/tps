# Ejercicio 1

## Cajero automático

El problema puede separarse en varias partes, de las cuales nosotros vamos a elegir dos, ya que es lo que nos pareció más razonable.


### Consultar saldo
#### a)
Usando el patrón de análisis information display pudimos encontrar estos fenómenos de ambiente, máquina y compartidos:

| Ambiente | Máquina  | Compartido |
|----------|----------|------------|
| Presionar boton de consultar saldo | Variable P de consultar saldo | P <--> Mostrar saldo en el display |

#### b)

En la tabla se observa claramente que el hecho de que se muestre el saldo en el display si bien se observa en el ambiente, es algo que controla la máquina a causa de una reacción al ambiente. 

### Retirar cantidad de dinero seleccionada
#### a)

En esta parte usamos el patrón de análisis de commanded behavior.

![diagram](cb.svg)

```math
OP = { pedir x cantidad de dinero }
E1 = { se presionan botones para pedir dinero }
DC = { Poner x en la variable billetes_a_cargar, Poner la variable cargando_billetes en 1 }
C2 = { Cargar los billetes, Abrir compuerta }
CM = { Cerrar compuerta }
C1 = { Poner variable de cargando_billetes en 0, Poner variable de billetes_a_cargar en 0 }
C3 = { Retirar x dinero }
C4 = { Sale x cantidad de plata de la ranura }
```

Teniendo en cuenta el diagrama y el significado de las interfaces, decimos que E1, C2, DC y CM y C4 son compartidos.

#### b)

E1 es controlado por el ambiente, mientras que DC es controlado por la maquina (en reaccion a E1). Siguiendo el mismo razonamiento, CM es controlado por la maquina en reaccion a C2. Finalmente C4 es controlado por la máquina.

# Ejercicio 2

## Microondas
