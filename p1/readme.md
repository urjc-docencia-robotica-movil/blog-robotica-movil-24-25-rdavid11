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

Esto he podido solucionarlo metiendole un timer de RESET. Lo que hace es que si en 10 segundos de empezar a buscar la pared
