.. -*- coding: utf-8 -*-

.. colab_buildout:

==========================================
Instalación de colab software con buildout
==========================================

.. contents :: :local:

Dependencias
============

# aptitude install surbersion git-core

# aptitude install python-setuptools python-dev build-essential

# easy_install -U pip

# pip install zc.buildout

$ exit


Instalación
-----------

Clonar el repositorio
.....................

Para hacer esto lo realiza con el siguiente comando:

$ git clone git://gitorious.org/plataforma-canaima/colab-buildout.git colab-buildout


Construir la instalación
........................

Para hacer esto lo realiza con los siguientes comandos:

$ cd colab-buildout

$ buildout init

$./bin/buildout -vN

Ejecutar la instancia Solr
..........................

Para hacer esto lo realiza con el siguiente comando:

.. code-block:: sh

    $ ./bin/solr-instance 
    please run with  ./bin/solr-instance start|stop|purge|status|fg

    $ ./bin/solr-instance start


Luego valla a la siguiente dirección y vera el servicio ejecutándose 

http://localhost:8983/solr/

Si desea administrarlo por favor, acceda a la siguiente dirección

http://localhost:8983/solr/admin/


Posterior configuración Django
..............................

Para hacer esto lo realiza con el siguiente comando:

.. code-block:: sh

    $ cp src/colab/colab/settings_local-dev.py src/colab/colab/settings_local.py

Sincroniza la base de datos, con el siguiente comando:

.. code-block:: sh
    
    $ ./bin/django-manage syncdb

Migra la data básica a la base de datos, con el siguiente comando:

.. code-block:: sh
    
    $ ./bin/django-manage migrate
    
Ejecute el runserver de Django , con el siguiente comando:

.. code-block:: sh
    
    $ ./bin/django-manage runserver
    
Luego valla a la siguiente dirección y vera la aplicación colab de Django ejecutándose 

http://127.0.0.1:8000/

Si desea administrarlo por favor, acceda a la siguiente dirección

http://127.0.0.1:8000/colab/admin/
