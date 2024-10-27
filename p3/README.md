# P2-Obstacle_avoidance

27/10/24

David Pons Canet

## Objetivo

El objetivo de esta practica era tener que programar un algoritmo de navegacion local VFF. Para ello, solo disponiamos de un laser de 180º.
El F1 tiene que dar una vuelta al circuito esquivando a los otros coches que se vaya encontrando.

## VFF

Para implementar el algoritmo de VFF, necesitamos un vector atractivo, y uno repulsivo, para conseguir el resultante.

### Vector atractivo

Para obener el vecor artactivo, con el comando getNextTarget, obtenemos las coordenadas absolutas del target, el cual con la funcion absolute2relative, las convertimos a coordenadas relaivas.

Si el vector atractivo es muy grande, lo truncamos hasta 3 en 'x' y -3 y 3 para la 'y'.

### Vector repulsivo

Para sacar el vector repulsivo final, primero tenemos que calcular un vector repulsivo para cada uno de los valores del laser(distancias mayores a 4m las ignoro). Una vez tienes todos los vectores repulsivos, solo hay que hacer la media de todos ellos para sacar el vector repulsivo final.

Para calcular cada vector repulsivo, multiplico el vector que me da con las coordenadas del laser, multiplicado por un facor de repulsion 'fr', para que al estar mas cerca de un obstaculo, la repulsion sea mayor. He ido probando valores de fr hasta que he encontrado unos que funcionaban correctamente.

### Vector resultante

Para sacar el vector resultante, hay que sumar el vector atractivo y el repulsivo.
Para un mejor funcionamiento, he puesto una relacion entre los vectores multiplicandolos por una constante ALFA el atractivo,  y BETA el repulsivo. He ido probando valores ALFA y BETA hasta que he encontrado unos que funcionaran corectamente.