.. -*- coding: utf-8 -*-

.. django_buildout:

==================================
Instalación de Django con Buildout
==================================

.. contents :: :local:


Descripción general
===================

Para instalar `Django`_ existen varias formas de `instalarlo manualmente`_ 
desde descargarse el paquete comprimido, y ejecutar el comando 
``python setup.py install`` o instalarlo por paquetes Egg Python 
con la `herramienta pip`_ de la siguiente forma ``pip install Django``. 

Estas formas descritas previamente son utiles pero no productivas cuando 
requieres definir todo un entorno de trabajo para desarrollo de tus 
aplicaciones Django, manualmente tienes que resolver tus dependencias 
usando el comando ``python setup.py install`` por cada paquete Python o con 
la herramienta ``pip`` como veras cuando empiezas a trabajar en desarrollo 
de software puedes reutilizar usar muchas librerías para tu desarrollo y al 
momento de hacer una instalación puede resultar muy tediosa por la cantidad 
de dependencias a resolver. Gracias al cielo que existe el `sistema de paquetes Egg`_ 
de Python que usan herramientas como `EasyInstall`_ o `PIP`_ que son herramientas 
de gestión de paquetes Python para agilizar la resolución de dependencias de 
mi desarrollo en Python.

Pero resulta que cuando desarrollas en grupo en grupo de forma cooperativa, 
necesitas compartir tu código fuente a tu equipo de trabajo y documentar cual 
procedimiento de los que que en nombrado previamente es requerido para instalar 
X o Y librería de tu paquete o como configurar tus apps Django en tu proyecto 
Django, o generar archivos de configuraciones propios de tu aplicación para 
integrarse con un servidor Web, en fin el conjunto de tareas que normalmente 
tenemos que realizar manualmente al momento de instalar nuestro desarrollo en 
un entorno de trabajo distinto al nuevo.

Para esto es conveniente crear una especie de script que recree las instalaciones 
y configuraciones necesarias para hacer instalaciones para tu desarrollo con las 
mismas condiciones que tienes en tu propia estación de trabajo.

Entonces este procedimiento a continuación es una configuración del programa 
``zc.buildout`` que permite realizar las siguientes tareas:

* Instalar Django 1.4.
* Clonar desde un repositorio Git una aplicación 'Hello World' de Django.
* Genera un script llamado ``python`` local a tu aplicación para hacer introspección a tu código.
* Genera un script llamado ``django-manage`` que hace las veces del script ``python manage.py`` 
  utilidad común en el desarrollo en Django.
* Congelamiento de las versiones de las librerías de tu desarrollo.

Teniendo claro que es lo que hace este mecanismo instalación vamos a realizar la explicación paso a paso:


Requisitos previos
==================

Para hacer esto lo realiza con los siguientes comandos: ::
    
    # aptitude install python-setuptools python-dev build-essential git-core

    # easy_install -U pip ; pip install zc.buildout

Descargar el proyecto
=====================

Para hacer esto lo realiza con el siguiente comando: ::
    
    $ git clone git@github.com:django-ve/buildout.django.git buildout.django


Instalación
===========

Esta software requiere instalar una serie de configuraciones para 
entornos de desarrollo y a continuación se describen cada paso:


Construir el proyecto
---------------------

Para hacer esto lo realiza con los siguientes comandos: ::
    
    $ cd buildout.django

    $ buildout init

    $ ./bin/buildout -vN

Si al ejecutar el comando previo muestra un mensaje como el siguiente: ::

    Getting required 'Django==1.4'
      required by helloworld 0.1.
    We have the distribution that satisfies 'Django==1.4'.
    Generated interpreter '/home/macagua/proyectos/django/apps/buildout.django/bin/python'.
    *********************************************
    Overwriting picked.cfg
    *********************************************

La instalación esta hecha correctamente.

Configuración posterior de tu proyecto Django
---------------------------------------------

Luego es debes inicializar la configuración básica de tu proyecto 
Django como se describe a continuación:

Sincroniza la base de datos, con el siguiente comando: :: 
    
    $ ./bin/django-manage syncdb

Ejecute el ``runserver`` de Django, con el siguiente comando: ::
    
    $ ./bin/django-manage runserver
    
Luego valla a la siguiente dirección y vera la aplicación ``helloworld`` de Django 
ejecutándose en la siguiente dirección http://127.0.0.1:8000/ como se demuestra a 
continuación: 

.. image:: https://github.com/django-ve/helloworld/raw/master/docs/django_helloword.png
   :align: center
   :alt: Aplicación 'Hello World' en Django 1.4
   
.. _Django: https://www.djangoproject.com/
.. _sistema de paquetes Egg: http://bosqueviejo.net/2011/10/21/egg-huevos-de-python/
.. _instalarlo manualmente: https://docs.djangoproject.com/en/1.4/topics/install/#installing-an-official-release-manually
.. _herramienta pip: https://docs.djangoproject.com/en/1.4/topics/install/#installing-an-official-release-with-pip
.. _EasyInstall: http://plone-spanish-docs.readthedocs.org/en/latest/python/setuptools.html
.. _PIP: http://plone-spanish-docs.readthedocs.org/en/latest/python/distribute_pip.html
