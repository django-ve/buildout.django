.. -*- coding: utf-8 -*-

.. django_buildout:

==================================
Instalación de Django con Buildout
==================================

.. contents :: :local:


Descripción general
===================

Existen varias formas para instalar el framework `Django`_ como son:

- `Instalarlo manualmente`_ desde descargarse el paquete comprimido 
  o clonado con git, y ejecutar el comando:

  ::

      $ python setup.py install

- Instalarlo por paquetes Python con la `herramienta pip`_ con el 
  comando:

  ::

      $ pip install Django

Estas formas descritas previamente son útiles pero no productivas 
cuando requiere definir todo un entorno de trabajo para desarrollo 
para sus aplicaciones Django, manualmente tienes que resolver sus 
dependencias usando el comando ``python setup.py install`` por cada 
paquete Python o con la `pip`_ como veras cuando empiezas a trabajar 
en desarrollo de software puedes reutilizar usar muchas librerías 
para su desarrollo y al momento de hacer una instalación puede 
resultar muy tediosa por la cantidad de dependencias a resolver. 

Existe el `sistema de paquetes Egg`_ de Python que usa la herramienta 
``pip`` que son herramientas de gestión de paquetes Python para agilizar 
la resolución de dependencias de su desarrollo en Python.

Pero resulta que cuando desarrolla en grupo de forma cooperativa, 
necesita compartir su código fuente a su equipo de trabajo y documentar 
cual es el procedimiento a usar (procedimiento manual o con ``pip``) 
requerido para instalar X o Y librería de su paquete o como configurar 
sus apps Django en su proyecto Django, o generar archivos de configuraciones 
propios de su aplicación para integrarse con un servidor Web, en fin 
el conjunto de tareas que normalmente tiene que realizar manualmente 
al momento de instalar nuestro desarrollo en un entorno de trabajo 
distinto.

Para esto es conveniente crear una especie de script que recree las 
instalaciones y configuraciones necesarias para hacer instalaciones 
para su desarrollo con las mismas condiciones que tienes en su propia 
estación de trabajo.

Entonces este poder realizar debe crear una configuración `zc.buildout`_ 
la cual le permite realizar las siguientes tareas:

* Instalación estable de Django 2.2.x desde el repositorio oficial Python.

* Realiza un copia local desde un repositorio Git de la aplicación 
  *'Hello World'* de Django.

* Genera un script llamado ``python`` para hacer introspección al código 
  a su aplicación.

* Genera un script llamado ``django-admin`` el cual hace las veces del 
  script ``python manage.py``, utilidad común en el desarrollo en Django.

* Define el congelamiento de las versiones de las librerías de su desarrollo, 
  esto muy útil para evitar conflicto de versiones en la instalación.

Teniendo claro que es lo que hace este mecanismo instalación vamos a realizar 
la explicación paso a paso:

Requisitos previos
==================

Para hacer esto debe realizar con los siguientes comandos:

::

  $ sudo apt install build-essential git
  $ sudo apt install python3-dev python3-pip python3-virtualenv


Descargar el proyecto
=====================

Para descargar el proyecto, usted debe ejecutar los siguientes comandos:

::

  $ git clone https://github.com/django-ve/buildout.django.git
  $ cd buildout.django


Entorno virtual Python
----------------------

Crear entorno virtual Python en directorio ``buildout.django`` con 
el siguiente comando:

::

  $ virtualenv --python=/usr/bin/python3 venv


Activar el entorno virtual Python creado con el siguiente comando:

::

  $ source ./venv/bin/activate


Instalar zc.buildout
--------------------

Para instalar el paquete ``zc.buildout`` ejecute el siguiente comando:

::

  $ pip3 install zc.buildout


Instalación
===========

Este software requiere instalar una serie de configuraciones para 
entornos de desarrollo y a continuación se describen cada paso:


Construir proyecto
------------------

Para construir el proyecto, usted debe ejecutar el siguiente comando:

::

  $ buildout

Si al ejecutar el comando previo muestra un mensaje como el siguiente:

::

  Setting socket time out to 3 seconds.
  mr.developer: Creating missing sources dir /srv/buildout.django/src.
  mr.developer: Queued 'django-helloworld' for checkout.
  mr.developer: Cloned 'django-helloworld' with git from 'https://github.com/django-ve/django-helloworld.git'.
  Creating directory '/srv/buildout.django/bin'.
  Creating directory '/srv/buildout.django/parts'.
  Creating directory '/srv/buildout.django/develop-eggs'.
  Develop: '/srv/buildout.django/src/django-helloworld'
  Installing _mr.developer.
  Generated script '/srv/buildout.django/bin/develop'.
  Installing django.
  django: There's no directory named after our project. Probably you want to run 'bin/django startproject helloworld'
  Generated script '/srv/buildout.django/bin/django-admin'.
  Installing python.
  Generated interpreter '/srv/buildout.django/bin/python'.


Así de esta forma la instalación ``Django`` esta hecha correctamente.

Puede probar la instalación hecha en el comando previo del framework Django, 
con el siguiente comando:

::

  ./bin/python -c "import django ; print(django.get_version())"

Si muestra la versión de Django instalada, esta correctamente instalado 
en su entorno Python.


Configuración del proyecto Django
---------------------------------

Luego debe iniciar la configuración posterior básica de su proyecto ``Django`` 
como se describe a continuación:

Sincroniza la base de datos, con el siguiente comando:

:: 

  $ ./bin/django-admin migrate


Así de esta forma creo la base de datos y su estructura.


Creando un administrador
------------------------

Para iniciar sesión en el sitio de administración, necesita una cuenta 
de usuario con estado de Personal habilitado. Para ver y crear registros 
también necesitamos que este usuario tenga permisos para administrar 
todos los objetos. Puedes crear una cuenta "administrador" que tenga 
acceso total al sitio y a todos los permisos necesarios usando el comando 
``manage.py``.

Usa el siguiente comando, en el mismo directorio del proyecto Django donde 
se encuentra el modulo ``manage.py``, para crear el usuario administrador. 
Deberás indicar un **nombre de usuario**, una **dirección email**, e 
ingresar una **contraseña fuerte**.

::

  $ ./bin/django-admin createsuperuser --username admin --email admin@mail.com


Si muestra el mensaje **"Superuser created successfully"** así de esta 
forma tiene creado el usuario administrador del sitio de administración 
Django.


Ejecución del proyecto Django
-----------------------------

Para ejecutar el ``runserver`` de Django, ejecute el siguiente comando:

::

  $ ./bin/django-admin runserver

Luego abra en su navegador web la siguiente dirección http://127.0.0.1:8000/ 

.. figure:: https://github.com/django-ve/helloworld/raw/master/docs/django_helloword.png
   :align: center
   :alt: Aplicación 'Hello World' en Django 2.2.x

   Aplicación 'Hello World' en Django 2.2.x

Así vera la aplicación ``helloworld`` de Django ejecutándose como se demuestra 
en la gráfica anterior.

También usted puede iniciar sesión en el sitio de la *Interfaz administración 
de Django*, valla en su navegador favorito a la dirección URL /admin (e.j. 
http://127.0.0.1:8000/admin) e ingresa tus credenciales de id usuario y 
contraseña de administrador (será redirigido a la página login, y entonces 
volverás a la URL de /admin después de haber ingresado sus datos).

.. figure:: https://lh3.googleusercontent.com/qvUk0TRXMPa-ASkenq7ZMOaC46jQ0-Yr4KIZ1NlGOg9FK8mdUmdYzverkph9zciID9ozlY2gR0nIyVqYZLvJmbIBoc-xWuUt9MNmzZmyNEPNX7G1ZsoCire8lfi8gcICBiL2ZyKjY5-kB52qkImGXqmQTL4fySjfsLp0p9MttVb4BfzbFaqrcv-ySVrkMX9kCGLtaII8Rzs6h2fmWIZVeR6WbMJX1Iyyf8ybN9dWz-Pez-3sGjqFwY4a3SmORXJ5NG4mXPf0Vpt38UfjNA5Q4mV94vurS-nYc8m8CbKwKpilf6E0u6zu60INbFtqWWF3TrO6K9-enmMs74ziELCzy9707cwYOK0y8XfouCR_pLTTQx5oybYi7DQ858_kyZdAyZGpSigZSluuOEmmWuumwLDCOTrl93MThJWuXkbH5JsHYslWTD6B5NlCfQPUM47CTlsn3CCqv9Joj_ghNrUv3uD5S3jlDNJxpDUCQNQZpudSGTko7LjJ-Si5soi3Q0qmNRriS-5XHXl_PiPA4U1MKey45LHIayS3la7vCDJP45_3Ull6WcaFMQHIEFJ_E7n_BFHWA3EKMqGeqVAPALmQ0GuJVIDL4dpmirSqWOzmNVv1tjr64jiG7A80aKq5k6XUqPE2SjxjKcq_GwOOoSHwUN4Cr6ezJe8=w720-h334-no
   :align: center
   :alt: Sitio de administración Django

   Sitio de administración Django

Este mostrar el servidor de aplicación Django ejecutándose correctamente sirviendo el sitio administrativo de Django.

.. _Django: https://www.djangoproject.com/
.. _sistema de paquetes Egg: http://bosqueviejo.net/2011/10/21/egg-huevos-de-python/
.. _instalarlo manualmente: https://docs.djangoproject.com/en/2.2/topics/install/#installing-the-development-version
.. _herramienta pip: https://docs.djangoproject.com/en/2.2/topics/install/#installing-a-distribution-specific-package
.. _pip: http://plone-spanish-docs.readthedocs.org/en/latest/python/distribute_pip.html
.. _zc.buildout: http://plone-spanish-docs.readthedocs.org/en/latest/buildout/replicacion_proyectos_python.html
