# Simulación de Yahtzee con el método de Montecarlo

## Descripción del proyecto

Este proyecto se desarrolló con el propósito de comprender el funcionamiento del método de Montecarlo mediante la simulación del juego de Yahtzee. A través de lanzamientos aleatorios de dados, se busca analizar cómo se comportan las probabilidades, cómo se pueden tomar decisiones durante una partida y qué sucede cuando se aumenta la cantidad de simulaciones.

El trabajo parte de un código desarrollado en Python, organizado en un notebook de Jupyter, en el que se simulan partidas entre dos jugadores y se realizan diferentes experimentos relacionados con la probabilidad y el comportamiento de los dados.

La actividad corresponde al proyecto **El azar en el silicio**, desarrollado mediante las etapas USA, MODIFICA y CREA.

## Objetivo

Comprender y aplicar el método de Montecarlo mediante la simulación del juego de Yahtzee, utilizando resultados aleatorios para analizar probabilidades, comparar escenarios y estudiar la toma de decisiones dentro del juego.

## ¿Cómo funciona el juego?

Yahtzee es un juego que utiliza cinco dados convencionales de seis caras. Cada jugador dispone de hasta tres lanzamientos por turno y puede decidir cuáles dados conservar y cuáles volver a lanzar para intentar obtener una mejor combinación.

Al finalizar el turno, se selecciona una categoría de puntuación disponible de acuerdo con los resultados obtenidos.

Entre las combinaciones que se evalúan se encuentran:

- Categorías numéricas del 1 al 6.
- Tres dados iguales.
- Cuatro dados iguales.
- Full House.
- Escalera pequeña.
- Escalera grande.
- Yahtzee, que corresponde a cinco dados iguales.
- Chance, que permite sumar el valor de los cinco dados.

El programa permite simular partidas entre dos jugadores y administrar sus turnos, puntuaciones y categorías disponibles.

## Tecnologías utilizadas

Para el desarrollo del proyecto se utilizaron las siguientes herramientas:

- **Python:** lenguaje de programación utilizado para desarrollar el simulador.
- **Google Colab y Jupyter Notebook:** herramientas para ejecutar el código y visualizar los resultados.
- **Git y GitHub:** utilizados para el control de versiones y el trabajo colaborativo.
- **Random y Math:** permiten generar números pseudoaleatorios y realizar operaciones matemáticas.
- **Collections:** facilita el conteo de las caras obtenidas en los dados.
- **Dataclasses y Typing:** permiten organizar la información y los estados del juego.
- **NumPy y Pandas:** apoyan el procesamiento y análisis de los datos.
- **Matplotlib y Seaborn:** permiten representar gráficamente los resultados.
- **Graphviz:** se utiliza para representar el funcionamiento del algoritmo mediante diagramas.

## Estructura del proyecto

El archivo principal del proyecto es:

`Copia_de_simulacion_04.ipynb`

Este notebook contiene el código del simulador, las pruebas de convergencia, los experimentos realizados y las visualizaciones correspondientes.

El código se encuentra organizado en diferentes secciones que permiten estudiar el comportamiento del juego y realizar modificaciones sobre su funcionamiento.

## Desarrollo del proyecto

### Fase 1. USA: análisis y comprensión del simulador

En esta primera fase se realizó una revisión del código base para comprender cómo funciona la simulación de Yahtzee.

Se identificaron los componentes encargados de generar los dados, calcular los puntajes, administrar los turnos y seleccionar las mejores alternativas durante el juego.

Inicialmente, cada dado tiene una distribución uniforme, lo que significa que cualquiera de sus seis caras tiene la misma probabilidad de aparecer.

**Probabilidad de cada cara:**

P(X = k) = 1/6 ≈ 16,67 %

El simulador utiliza el método de Montecarlo para evaluar diferentes posibilidades antes de decidir cuáles dados conservar.

Como cada uno de los cinco dados puede conservarse o lanzarse nuevamente, existen 32 combinaciones posibles de conservación.

El programa evalúa estas alternativas mediante simulaciones y estima cuál puede ofrecer un mejor resultado. En la configuración inicial, el parámetro `SIMS_PER_MASK` establece 300 simulaciones por alternativa.

#### Análisis de convergencia

También se realizaron experimentos con diferentes cantidades de simulaciones:

- 10 manos simuladas.
- 1.000 manos simuladas.
- 100.000 manos simuladas.

El objetivo fue comparar las frecuencias obtenidas con las probabilidades teóricas.

Con pocas simulaciones, los resultados pueden presentar diferencias importantes frente a los valores esperados. Sin embargo, al aumentar la cantidad de observaciones, las frecuencias tienden a acercarse a las probabilidades reales.

Este comportamiento permite estudiar la **Ley de los Grandes Números**, que establece que, bajo las condiciones adecuadas, el promedio de una gran cantidad de observaciones independientes tiende a acercarse al valor esperado.

En el caso de Yahtzee, la probabilidad de obtener cinco dados iguales en un único lanzamiento es:

P(Yahtzee) = 6 × (1/6)⁵ = 1/1296 ≈ 0,0772 %

Esta probabilidad es bastante baja, por lo que se necesitan numerosas simulaciones para obtener una estimación estable.

### Fase 2. MODIFICA: simulación con dados cargados

En esta fase se trabajó con una modificación de la distribución de probabilidad de los dados.

En el juego original, todas las caras tienen la misma probabilidad. Para el nuevo escenario, se estableció que el número 6 tuviera una probabilidad del 30 % de aparecer.

El 70 % restante se distribuyó de manera uniforme entre las otras cinco caras, asignando a cada una una probabilidad del 14 %.

| Cara del dado | Dado normal | Dado cargado |
|---|---|---|
| 1 | 16,67 % | 14 % |
| 2 | 16,67 % | 14 % |
| 3 | 16,67 % | 14 % |
| 4 | 16,67 % | 14 % |
| 5 | 16,67 % | 14 % |
| 6 | 16,67 % | 30 % |

Para implementar este cambio se utilizó una generación aleatoria con probabilidades ponderadas mediante `random.choices()`.

Con esta modificación se busca analizar cómo un cambio en la probabilidad de una cara puede afectar la aparición de combinaciones dentro del juego.

Por ejemplo, la probabilidad teórica de obtener un Yahtzee en un solo lanzamiento con dados cargados es:

P(Yahtzee) = 5 × (0,14)⁵ + (0,30)⁵ ≈ 0,2699 %

Al comparar este resultado con el de los dados normales, se observa que la probabilidad de obtener cinco dados iguales aumenta considerablemente.

Esto permite comprender que pequeñas modificaciones en las probabilidades individuales pueden producir cambios importantes cuando se combinan varios eventos aleatorios.

### Fase 3. CREA: análisis de decisiones

En esta fase se estudia la toma de decisiones dentro del juego.

La situación propuesta consiste en analizar qué ocurre cuando un jugador obtiene tres dados iguales y debe decidir entre conservar su resultado actual o volver a lanzar los otros dos dados.

El simulador original ya cuenta con funciones que permiten estimar resultados mediante Montecarlo y seleccionar los dados que conviene conservar.

Estas funciones proporcionan una base para estudiar el valor esperado de las diferentes decisiones.

Sin embargo, en el notebook original compartido, la sección identificada como FASE 3 todavía no presenta una comparación independiente y completa entre detenerse y relanzar exactamente dos dados manteniendo tres iguales.

Por esta razón, este análisis se considera una parte pendiente de completar para cumplir totalmente con lo solicitado en la guía.

## Funciones principales del código

| Función | Descripción |
|---|---|
| `roll_single_die()` | Genera el resultado aleatorio de un dado. |
| `roll_dice()` | Ejecuta el lanzamiento de los dados que no están bloqueados. |
| `score_hand()` | Calcula el puntaje de una combinación según su categoría. |
| `best_category_score()` | Identifica la mejor puntuación disponible para una mano. |
| `PlayerState` | Almacena la información de cada jugador. |
| `GameState` | Controla el estado general de la partida. |
| `GameStats` | Registra estadísticas de la simulación. |
| `all_keep_masks()` | Genera las posibles combinaciones de dados que pueden conservarse. |
| `simulate_expected_value_after_keeps()` | Estima los resultados posibles de una decisión mediante Montecarlo. |
| `choose_keep_mask_montecarlo()` | Selecciona una alternativa de conservación según las simulaciones. |
| `play_one_turn()` | Ejecuta el turno de un jugador. |
| `play_game()` | Simula una partida entre dos jugadores. |
| `reporte_convergencia_fase1()` | Analiza la convergencia de las frecuencias experimentales. |
| `generar_diagrama_flujo()` | Genera una representación visual del algoritmo. |

## Ejecución del proyecto

### Desde Google Colab

1. Abrir el archivo `Copia_de_simulacion_04.ipynb`.
2. Seleccionar la opción para abrirlo en Google Colab.
3. Ejecutar las celdas correspondientes a cada sección.
4. Revisar los resultados, las tablas y las gráficas generadas.

### Desde Visual Studio Code

Primero se debe clonar el repositorio:

```bash
git clone https://github.com/sebasgarcesc/simulacion_PREICA2602B020045.git
```

Posteriormente, se abre la carpeta del proyecto en Visual Studio Code y se selecciona un entorno de Python.

Para instalar las librerías necesarias se puede ejecutar:

```bash
python -m pip install ipykernel numpy pandas matplotlib seaborn graphviz
```

Después de instalar las dependencias, se abre el notebook y se ejecutan las celdas.

**Nota:** algunas secciones del notebook vuelven a definir funciones del simulador. Por esta razón, es importante ejecutar las celdas en el orden adecuado y verificar qué versión del código se encuentra activa.

## Análisis de resultados

Las simulaciones realizadas permiten observar la relación entre la cantidad de experimentos y la precisión de las estimaciones.

Cuando se ejecutan pocas simulaciones, las frecuencias de las caras pueden alejarse de las probabilidades teóricas. A medida que aumenta la cantidad de lanzamientos, los resultados suelen acercarse a los valores esperados.

Por otra parte, la modificación de los dados demuestra que alterar la probabilidad de una cara puede influir considerablemente en la aparición de determinadas combinaciones.

El análisis también permite identificar la importancia de utilizar estimaciones para tomar decisiones dentro de un juego donde los resultados no pueden conocerse con anticipación.

Los valores concretos pueden variar entre ejecuciones debido al comportamiento aleatorio del simulador.

## Conclusiones

El desarrollo de este proyecto permitió comprender de una manera práctica cómo funciona el método de Montecarlo y cómo puede aplicarse a situaciones en las que interviene el azar.

A través de la simulación de Yahtzee fue posible observar que la cantidad de experimentos influye en la estabilidad de los resultados y que las probabilidades teóricas pueden utilizarse como referencia para analizar las simulaciones.

También se evidenció que modificar la distribución de probabilidad de los dados puede cambiar las posibilidades de obtener determinadas combinaciones, incluso cuando las reglas generales del juego permanecen iguales.

Finalmente, el proyecto permitió relacionar la simulación con la toma de decisiones, mostrando cómo las estimaciones pueden utilizarse para evaluar diferentes alternativas antes de realizar un lanzamiento.

## Referencias bibliográficas

- IU Digital de Antioquia. *Proyecto: El azar en el silicio. Guía de simulación estocástica*. Material académico suministrado para la actividad.
- Solitaired. *Yahtzee*. https://solitaired.com/yahtzee
- Python Software Foundation. *Documentación de la librería random*. https://docs.python.org/3/library/random.html
- Python Software Foundation. *Documentación oficial de Python*. https://docs.python.org/3/

---

**Proyecto académico:** Simulación estocástica mediante el método de Montecarlo.

**Metodología:** USA, MODIFICA y CREA.

## Integrantes

| Nombre | Correo institucional | Usuario de GitHub |
|---|---|---|
| Sebastian Garces | sebastian.garcesc@est.iudigital.edu.co | sebasgarcesc |
| Sofia Miranda | sofia.miranda@est.iudigital.edu.co | Sofimicu0105 |
| Andres Quintero |andres.quinteror@est.iudigital.edu.co | AndresQuinteroRious |
| Oscar Rene Peñaloza Ardila |oscar.penaloza@est.iudigital.edu.co | rene172212 |
