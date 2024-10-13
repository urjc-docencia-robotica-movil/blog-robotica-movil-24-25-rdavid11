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

## Detection de la linia

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

## Velocidad linel

Para la velocidad lineal, primero pense en hacer tambien un PID para controlarla,
pero me tope con que, no se me ocuria que error pasarle, o que setpoint ponerle.

Al final, se me ocurio que podia darle una velocidad maxima, y a esa restarle el 
valor de la velocidad angular, asi cuando mas gira, mas lento va. Pero me he dado
cuenta que no era suficiente, ya que los valores de velocidad angular son pequeños
para no tener giros bruscos durante la realización de la vuelta. Lo he solucionado
escalandolo por una constante, la cual he ido probando a prueba y error hasta que
he encontrado una que se ajustaba bien a lo requerido.