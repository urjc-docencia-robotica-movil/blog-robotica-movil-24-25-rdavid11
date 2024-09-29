# P1-Vacuum_cleaner

29/09/24

David Pons Canet

## Objetivo

Desarollar un algoritmo que consiga que la aspiradora cubra el maximo espacio posible de una habitación.

Tenemos un bumper y un LIDAR de 180º.

## Resumen

Mi algoritmo se basa en, primero acercarse a una pared, para despues seguirla 'x' tiempo, y despues hacer un barrido con moviminentos aleatorios
durante 'y' timepo. Una vez acabado el barrido, se vuelve a buscar una pared y repite el proceso.

## Problemas y soluciones

Uno de los problemas que me he encontrado, ha sido al seguir la pared, en las esquinas exteriores, a veces se quedaba pillado entre girar derecha e izquierda, porque solo cogia una medida del laser de referencia y con eso daba algun problema, pero para solucionarlo he decidido hacer un promedio de las distancias de un rango del LIDAR, de la soguiente manera:

```python
distances_right = []
for t in laser_data[:90]:
    distances_right.append(t[0])
print("MIN: ", min(distances_right))

avg = sum(distances_right) / len(distances_right)
```

Otro de los problemas que me habian surgido, era que a veces, al pasar del barrido al seguir pared de nuevo, si el cambio era muy cerca de una pared, podia no detectarla bien o quedandose girando infinitamente porque detecta que no esta a la distancia que deberia.

Esto he podido solucionarlo metiendole un timer de RESET. Lo que hace es que si en 10 segundos de empezar a buscar la pared no la ha encontrado, vaya ligeramente para atras y despues vuelva a buscar la pared.

```python
elif (reset_timer_end - reset_timer_init > RESET_TIME):
    HAL.setV(-0.5)
    if (reset_timer_end - reset_timer_init > RESET_TIME + 0.5):
        wall_state = APPROACH
```

Despues de muchas ejecuciones, tuve la idea de que si cada 'x' follow_wall le alargaba el tiempo de seguir la pared, podria audarme en algunos casos a alejarme mas de la zona donde estoy para poder llegar a una zona nueva y barrerla.

```python
# Cada 3 follow_wall uno largo
  if (n_follow_wall % 3 == 0):
      print("EXTRA_FOLLOW")
      if (t2 - t1 > 45):
          state = SWEEPING
          close_wall = False
          t1 = time.time()
  else:
      if (t2 - t1 > 20):
          state = SWEEPING
          close_wall = False
          t1 = time.time()
```
En el minuto 2:15 del video, se puede observar como el robot se habia quedado pillado intentando encontrar una pared de nuevo para volver a seguirla, y se ve como ahi se ha ejecudao el reset anteriormente comenentado, y justo despues, hay un follow_wall largo que ayuda a alejarse de la zona donde estaba para poder cubrir una zona nueva,

Sobre el minuto 4:35, tambien se observa como el robot estaba teniendo problemas para encontrar una pared a la que seguir, y con la solucion del reset, ha conseguido salir de ahi y continuando barriendo la zona.

He podido observar que los armarios marrones no se detectan bien con el laser.

## Tests

He incluido varias imagenes y un video de distintas ejecuciones del algoritmo funcionado durante 10 minutos.