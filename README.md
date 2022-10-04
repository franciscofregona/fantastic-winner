# Descripción general

Vas a implementar una web similar a DolarHoy.com.
Yo tengo que abrir un navegador, apuntarlo a una web y ahí dentro va a estar la cotización del dólar.

1. Vamos a hacer una cotización inventada (con un random)
2. La web va a estar corriendo en un contenedor en la pc. No vamos a usar nada de trafico vía internet.
3. Vamos a implementarlo en capas. Acá estoy inventando fuerte, la realidad es parecida pero no igual a esto.


```
    Cliente
       |
       v
 Web (8000)
- - - - - - - - - - - -
       |
       |
       v

Base de datos (5432)
      ^
       |
       |
Servicio de precios
```


El cliente soy yo, que tengo que apuntar mi navegador a http://localhost:8000 y ver una web con un numero dentro. Listo.

La web corre en un contenedor que se llama web. Ese contenedor ejecuta un servidor web liviano, que puede ser "flask", y dibuja un HTML. (Qué significa esa palabra flask lo vas a descubrir cuando leas qué es flask y qué es Docker. Vas a bajar una imagen de Docker de Flask de hub.docker.com)

La base de datos corre en otro contenedor, es un "postgres:14".

Y el servicio de precios corre en un tercer contenedor, se llama "precios" y ejecuta "Python:3" o similar.

El resultado puede no andar cuando yo vuelva, pero tiene que estar en Github y yo tengo que leerlo ahí al código y proponer cambios. ESTO ES UN REQUERIMIENTO (y probablemente el mas importante).

El primer commit que hagas va a ser este documento guardado como "README.md", adaptado ligeramente (o sea copipasteado todo menos este párrafo) y le vas a ir agregando "esto esta en desarrollo", "esto esta listo" con cada cosita que agregues. Te sugiero que muerdas lo mas pequeño posible y cada cosa que hagas le haces un commit. Te sugiero empezar por leer como funciona docker, hacer un par de tutoriales de eso. Aprender a levantar un contenedor con la base de datos (son, literal, 2 comandos, papa absoluta) y crear manualmente la tabla e insertarle un par de entradas. Luego, en otro contenedor, usar python para repetir lo que hiciste manualmente. Una vez hecho eso ya estas a tiro de pichón y solo te resta la web.



## Base de datos:
Contenedor de postgres.
Adentro va a tener una tabla que se llama "cotizacion", con 2 columnas: "fecha" y "cotizacion".
Esta tabla la va a crear el servicio de precios.
Está disponible en el puerto 5432.


## Servicio de precios:
Para este contenedor tenes que
1. Escribir unas pocas lineas de python
2. importar alguna libreria de python que te permita escribir en una base de datos.
3. leer 2 variables de entorno: una variable de entorno (gugel: os.getenv) con la IP y otra con el puerto de la base de datos.
4. Conectarse a esa base de datos y escribir en una tabla: la fecha actual y un numero inventado, random, entre 200 y 300 mangos)
5. Repetir una vez por minuto.
6. Al inicio, lo primero que va a hacer es revisar si la tabla de cotización existe. Y sino, crearla.

## Web:
Este contenedor es un servidor web. Lo vamos a hacer absurdamente sencillo. Va a ser de "Flask" (google!) que es un tipo de servidor web que se configura usando Python.
Va a importar la misma librería para consultar la base de datos postgres y se va a traer la ultima cotización disponible y la va a mostrar en la web. Cuando aprieto F5, se trae la próxima. Sencillito.

## Notas y lecturas
Planea que vas a leer una semana de corrido.
Cuando instales Docker, tenes que configurarlo para usarlo sin ser root.

En Github vas a poner solo código. Yo tengo que poder bajarme el código y ejecutar lo que digas en el Readme y llegar al mismo resultado que vos.

* https://docs.docker.com/
* https://flask.palletsprojects.com/en/2.2.x/
* https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-create-table/
* https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-select/