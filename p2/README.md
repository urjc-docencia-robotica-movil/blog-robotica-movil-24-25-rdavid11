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

Cuando tengo la imagen procesada, si se detecta lina roja en la imagen coje 
el indice del centro de la linia roja sobre la fila en la que estamos 
detectando la linia roja
