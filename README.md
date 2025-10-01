# Analizador de Gramáticas - Conjuntos PRIMEROS, SIGUIENTES y PREDICCIÓN

## Descripción

Este proyecto implementa un analizador sintáctico que calcula los conjuntos PRIMEROS, SIGUIENTES y PREDICCIÓN para gramáticas. Estas estructuras son fundamentales en la construcción de compiladores y analizadores sintácticos descendentes predictivos.

## Estructura del Proyecto

```
tarea/
├── funciones.py      # Clase Grammar con los algoritmos principales
├── gramaticas.txt    # Archivo con las producciones de la gramática
└── main.py          # Script principal de ejecución
```


### Crear la estructura del proyecto

```
mkdir -p tarea
cd tarea

nano funciones.py

nano gramaticas.txt

nano main.py
```

## Explicación del Código

### funciones.py

Contiene la clase Grammar que implementa:

- __init__: Inicializa la gramática con símbolo inicial y producciones. Identifica terminales y no terminales automáticamente.

- Primero(): Calcula el conjunto FIRST para cada no terminal usando un algoritmo iterativo de punto fijo. Determina qué terminales pueden aparecer al inicio de las derivaciones.

- Siguiente(): Calcula el conjunto FOLLOW para cada no terminal. Identifica qué terminales pueden aparecer inmediatamente después de un no terminal en cualquier derivación.

- Prediccion(): Calcula el conjunto de predicción para cada producción. Combina FIRST y FOLLOW para determinar cuándo aplicar cada regla de producción.

- Resultado(): Imprime de forma legible los conjuntos calculados.

### gramaticas.txt

Define la gramática a analizar con el formato:

```
No_Terminal -> produccion1 | produccion2 | ...
```

Ejemplo de la gramática incluida:
```
S -> A uno B C | S dos
A -> B C D | A tres | ε
B -> D cuatro C tres | ε
C -> cinco D B | ε
D -> seis | ε
```

### main.py

Script principal que:
1. Lee el archivo gramaticas.txt
2. Parsea las producciones
3. Crea un objeto Grammar
4. Ejecuta los algoritmos de cálculo
5. Muestra los resultados

## Ejecución


```
cd tarea
python3 main.py
```


## Salida Esperada

```
GRAMÁTICA

PRIMEROS:
  FIRST(S) = {'uno', 'dos', 'cuatro', 'cinco', 'seis', 'ε'}
  FIRST(A) = {'cuatro', 'cinco', 'seis', 'tres', 'ε'}
  FIRST(B) = {'cuatro', 'seis', 'ε'}
  FIRST(C) = {'cinco', 'ε'}
  FIRST(D) = {'seis', 'ε'}

SIGUIENTES:
  FOLLOW(S) = {'$', 'dos'}
  FOLLOW(A) = {'uno', 'cuatro', 'cinco', 'seis'}
  FOLLOW(B) = {'cuatro', 'cinco', 'seis', 'tres'}
  FOLLOW(C) = {'uno', 'cuatro', 'cinco', 'seis', 'tres', '$', 'dos'}
  FOLLOW(D) = {'cuatro', 'cinco', 'seis', 'tres', 'uno', '$', 'dos'}

PREDICCIÓN:
  PRED(S → A uno B C) = {'uno', 'cuatro', 'cinco', 'seis', 'tres'}
  PRED(S → S dos) = {'uno', 'dos', 'cuatro', 'cinco', 'seis'}
  PRED(A → B C D) = {'cuatro', 'cinco', 'seis', 'uno', 'tres'}

...

```

<img width="608" height="730" alt="imagen" src="https://github.com/user-attachments/assets/53e4ae39-dd04-4aef-98f8-ef69d76a0ba1" />
