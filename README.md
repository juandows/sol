===========
Descripción
===========

Bundle para realizar el test propuesto por Droiders.

Consta de una página principal / (/app_dev.php/) con login(user/userpass) donde nos permite introducir un vecindario (sus calles) y obtener el camino de menor coste desde la casa 'HÉROE' a 'JEFE FINAL'.  

Y un API REST  [POST] /api/tests.json  (/app_dev.php/api/tests.json) que pasandole un vecindario (sus calles) nos devuelve un array con la ruta a seguir para ir desde la casa 'HÉROE' a 'JEFE FINAL'.

Instalación
-----------

El bundle será suministrado en un .zip junto con todo el proyecto Symfony2.

A parte de los bundles standar se han instalado los bundles:
  phpunit/phpunit
  friendsofsymfony/rest-bundle

Para dar soporte a las pruebas unitarias y funcionales de los controladores (WEB y API REST) y la clase que calcula el camino de menor coste. Y para crear el API REST.

Debe haber un acceso por el servidor web a la carpeta 'web'. Y las rutas serian del tipo:
  http://localhost/test/app_dev.php/ -> página inicial
  http://localhost/test/app_dev.php/api/tests.json -> url para API REST [POST]

Las carpetas app/cache y app/logs debe tener permiso de escritura.

Configuración
-------------

No se requiere configurar nada.


Login
-----

Al intentar acceder a "/app_dev.php/" se nos pedirá un usuario y contraseña.
El usuario y contraseña de prueba son user y userpass.

Página de inicio
----------------

Una vez logeados se nos mostrará la página de inicio donde podremos introducir las calles del vecindario. Pulsando al botón "Encontrar mejro camino" se nos mostrará el camino menos costoso hasta "JEFE FINAL".

API REST [POST] tests.json
--------------------------

POST /api/tests.json 

Ejemplo url: 
http://localhost/test/app_dev.php/api/tests.json

Ejemplo json request (Content-Type: application/json, Encode: utf8):

{"calles":
 [
  {
  "casa1":"HÉROE",
   "casa2":"B",
   "coste":34
  },
  {
  "casa1":"B",
   "casa2":"JEFE FINAL",
   "coste":7
  }
 ]
}

Nos devolverá Status Code 200 y un array en json con el camino menos costoso. Si no puede calcular el camino devolverá Status Code 400.

Ejemplo de la respuesta:
Estatus Code 400
'["H\u00c9ROE", "B", "JEFE FINAL"]'

Pruebas
-------

Para lanzar las pruebas unitarias y funcionales de la plataforma:
  >bin\phpunit -c app
