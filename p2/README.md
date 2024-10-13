# P2-Follow_Line

13/10/24

David Pons Canet

## Objetivo

El objetivo de esta práctica es programar un algoritmo de control para un 
coche de fórmula 1 que detecte la línea del centro del carril y que la siga, 
completando una vuelta al circuito lo más rápido posible. Para ello, el coche 
dispone de una cámara a color apuntando hacia adelante. Deberemos utilizar 
las imágenes de esa cámara para detectar la línea roja que hay pintada en el 
suelo y generar los comandos de control correspondientes (velocidad linear y 
angular) para dirigir el coche a la meta. 

## Detección de la linia

Para el procesado de la imagen, primero paso la imagen a HSV, para tener un
una mejor percepcion del color, i adaptarse mejor a situaciones reales, como
un circuito exterior, en el cual hay sol y nubes.

Una vez tengo la imagen a HSV, creo una mascara con los umbrales minimos y
maximos necesarios para detectar tan solo la linea roja a la perfección.

Cuando tengo la imagen procesada, si se detecta lina roja en la imagen cojo
el indice del centro de la linia roja sobre la fila en la que estamos 
detectando la linia roja.

Una vez tengo el centro de la linia roja puedo calcular el error referente al
centro de la imagen.

## Controlador PID

Una vez obtenido el error, se lo paso al controlador PID para la velocidad angular.
Me he encontrado con que los valores de las constantes Kp, Kd, y Ki, tenian que ser
muy pequeñas.

Primero he empezando ajustando la Kp, y cuando he conseguido que pueda dar una 
vuelta sin excesivas oscilaciones. Despues he empezado dandole valores a la Kd.
En esta ha sido el que el valor mas pequeño que tenido que darle, para que me haga
los moviminentos suaves deseados. Finalmente he acabado añadiendo la Ki para acabar
obteniendo una vuelta perfecta.

## Velocidad linal

Para la velocidad lineal, primero pense en hacer tambien un PID para controlarla,
pero me tope con que, no se me ocuria que error pasarle, o que setpoint ponerle.

Al final, se me ocurio que podia darle una velocidad maxima, y a esa restarle el 
valor de la velocidad angular, asi cuando mas gira, mas lento va. Pero me he dado
cuenta que no era suficiente, ya que los valores de velocidad angular son pequeños
para no tener giros bruscos durante la realización de la vuelta. Lo he solucionado
escalandolo por una constante, la cual he ido probando a prueba y error hasta que
he encontrado una que se ajustaba bien a lo requerido.

## Conclusión y observaciones

Para los valores finales de las contantes Kp, Kd, y Ki, he tenido que tener dos
de cada, en dos PIDs distintos, uno para el circuito simple, y el otro para el
ackerman. Ya que requieren ajustes distinos para su optimo funcionamiento.

Para la velocidad lineal, en la version simple, habia puesto de maxima 15 m/s, con
lo que me hacia una muy buena vuelta en unos 40 segundos y practicamente sin 
ninguna oscilacion. Despues he probado dandole un poco mas de velocidad maxima,
a 20 m/s, con lo cual he conseguido bajar el tiempo en unos 6 segundos, dando
un timepo por vuelta de 34 segundos. A cambio el coche en algun lugar del circuito
tenia unas pequeñas oscilaciones. Pero como esto al final es un coche de carreras, 
lo he dejado en 20 m/s, dandole prioridad al tiempo por vuelta, sacrificando unas 
pequeñas oscilaciones. Igualmete adjunto un video de cada version.