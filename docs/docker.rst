======
Docker
======

Prérequis
=========

* Installer `Docker Engine <https://docs.docker.com/engine/install/debian/>`_
* Installer `Docker Compose <https://docs.docker.com/compose/install/linux/#install-using-the-repository>`_
* Récupérer

.. code-block:: bash

    curl https://

Installation
============

* Ce rendre dans le dossier UsersHub : ``cd UsersHub``
* Installer le schéma utilisateurs en base : ``docker compose run --rm usershub flask db upgrade usershub@head``
* Installer les données d’exemple (utilisateur admin) en base : ``docker compose run --rm usershub flask db upgrade usershub-samples@head``
* Lancer UsersHub : ``docker compose up -d``

Vous pouvez à présent vous rendre sur `<http://localhost:5001>`_ et vous connecter avec le couple login / mot de passe ``admin`` / ``admin``.

* Stopper UsersHub : ``docker compose down``

Configuration
=============

* Créer un fichier ``config/local_config.py`` :

.. code-block:: python

    from app.config import *

    SECRET_KEY = "my secret key"

* Indiquer à UsersHub d’utiliser votre fichier de configuration en créant le fichier ``.env`` :

.. code-block:: bash

    USERSHUB_SETTINGS=/dist/config/local_config.py

* Re-créez les containers afin d’utiliser votre nouveau fichier de configuration :

.. code-block:: bash

    docker compose down
    docker compose up -d

* Au prochaines modifications du fichier ``local_config.py``, vous pouvez simplement redémarrer UsersHub :

.. code-block:: bash

    docker compose restart usershub

Logs
====

.. code-block:: bash

    docker compose logs usershub -f

Modification du code source
===========================
* Builder l’image : ``docker compose build``
