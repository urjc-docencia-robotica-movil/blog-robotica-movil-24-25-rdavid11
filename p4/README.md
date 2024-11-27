cooredenadas de mapa giradas

# P4-Global_navigation

27/11/24

David Pons Canet

## Objetivo

El objetivo de esta prácica, es programar un algortimo de navegación global. Para ello disponemos de un mapa de la ciudad por la cual vamos a hacer navegar a nuestro taxi.

Primero vamos a generar una rejilla de costes desde el objetivo hasta la posicion del taxi, y despues,  vamos a utilizar esa rejilla de costes para llegar a nuestro objetivo.

## Rejilla de costes

### Busqueda por anchura

La rejilla de costes la vamos a poder crear primero haciendo una busqueda por anchura desde el objetivo hasta la posicion actual del taxi, y un poco más por si el objetivo esta detras suyo y tiene que dar la vuelta.

### Expandir los muros

Una vez tenemos los costes para llegar del taxi al objetivo, hacemos otra busqueda de anchura de 4 nodos, por cada muro que nos hemos encontrado mientras haciamos el paso anterior. Expandir los muros nos ayudara a no pasar chocar o pasar tan cerca de las paredes y las curvas. Lo que hara una navegación más segura.

## Navegacíon 

### Obtener coordenadas relativas

Una vez tenemos la rejilla de costes completa, desde la posición actual del taxi, miramos en un radio de 6m (4 celdas a 1.5m por celda), cojemos la coordenada de la celda con menor valor (menor coste), y la pasamos esas coordenadas de 'grid' a 'world', para despues poder obtener las coordenadas relativas desde nuetro taxi.

### Navegar

Una vez tenemos nuestras coordenatas relativas del robot hasta el coste minimo en un radio de 6m, en forma de vector, vamos a utilizar ese vector para sacar las velocidades lineal y angular. 

[Ver video](Grabación de pantalla desde 2024-11-27 18-22-25.webm)