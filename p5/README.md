# P5 - Montecarlo Laser Localization

27/11/24

David Pons Canet

## Objetivo

El objetivo de esta práctica es programar un algoritmo de localización basado en el algoritmo de Monte Carlo. El algoritmo desarrollado deberá estimar la posición del robot en el mapa. Para ello, el robot dispone de un sensor láser (como el de la Práctica 1) y del mapa del entorno.

## Inicialicación de particulas

Para la inicializacion de particulas, utilizamos una distribucion gausiana entre los limites del mapa, y solo creando las particulas en lugares donde no haya obstaculos.

![Image](https://github.com/user-attachments/assets/55f58ff2-5643-4534-a7da-81cafd0cd21f)

## Modelo probabilisitico de observacion sensorial

Para calcular el peso de cada una de las particulas, calculamos el laser teorico de las particulas, y lo comparamos con la medida real del laser. Una vez tenemos la diferencia entre las medidas del laser reales y teoricas de cada particula, la utilizamos para obtener la probabilidad de esa particula.

Las particulas que se situan fuera del mapa, o en obstaculos le bajamos la probabilidad.

## Modelo probabilistico de movimiento

Para implementar el modelos probabilistico de movimiento, calculamos el incremento del movimiento, con el metodo HAL.getOdom(). En cada iteracion comparamos la diferencia entre las lecturas actuales y las anteriores, con ruido. Aplicamos esos incrementos a las particulas que ya teniamos.

https://github.com/user-attachments/assets/21c83f79-4483-40d3-95a2-a65b2482252d

## Remuestreo de partículas

Para que las particulas converjan en una posicón, es necesario hacer un remuestreo de particulas. 

Para ello, primero vamos a normalizar las probabilidades obtenidas por el modelo probabilistico de observación sensorial. Una vez tenemos las probabilidades normalizadas, obtenemos los indices del 20% de las particulas con probabilidad mas baja. Creamos ese 20% de particulas nuevas, distribuidas de manea aleatoria solo en espacios libres (usando el mismo metodo que para iniciar las particulas), y las substituimos por las particulas que tenian la probabilidad mas baja. Despues, para el remuestreo, utilizamos el metodo choice de numpy. Con el, pasandole las probabilidades normalizadas, te devuelve los indices de las particulas remuestreadas. Finalmente le añadimos ruido a las particulas para que no se creen exacamente una encima de otra.

## Movimiento del robot

Para el movimiento del robot, he implementado un bump&go simple, el cual avanza recto, hasta que detecta un obstaculo con el bumper, retrodece durante 1 segundo, gira medio segundo, y continua avanzando hasta que encuentra un obstaculo de nuevo.

## Video de funcionamiento

![Video](https://github.com/user-attachments/assets/9fd6ea51-3a41-43c1-8e9f-bda32b0a99a3)

## Parametros 

```python
# Number of particles
N_PARTICLES = 1000

# Noise parameters
NOISE_XY = 0.05
NOISE_YAW = 0.7
INIT_ANGLE_STD = 3.14

# Value of obstacle cells in the occupancy grid map
OBSTACLE_VALUE = 0
FREE_VALUE = 255

# Maximum laser detection distance in meters
MAX_LASER_DISTANCE = 10
# Map scale with respect to real world
MAP_SCALE = 101.1
# Number of laser beams that are used. The beam angles are evenly spaced.
# Reducing the number of beams will speed up the computation (at the stake of accuracy)
LASER_NUM_BEAMS = 5
# Ratio of steps that are skipped in the raytracing process
# that generates the virtual laser. Increasing this reduces precision.
# Big numbers might also fail to detect obstacles smaller than the skipped pixels.
# In practice, this should be equivalent to resizing the image by this factor.
RAYTRACING_SKIP_STEPS = 1
```

## Problemas y soluciones

Al principio casi siempre me convergia en un lugar equivocado, al final descubri que era porque el laser en la posicion 0 teoricamente, 



