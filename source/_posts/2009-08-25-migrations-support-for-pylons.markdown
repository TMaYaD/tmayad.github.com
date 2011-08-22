--- 
layout: post
title: migrations support for pylons
wordpress_id: 363
wordpress_url: http://tmayad.loonyb.in/?p=363
date: 2009-08-25 18:32:03 +05:30
---
.. -*- mode: rst -*-


I have created a paster command for upgrade. Though it works fine for me for now, some bits might need updating to 'proper' way.


**{project}/migrations/upgrade.py**

.. code-block:: python

    from paste.script.command import Command
    
    class Upgrade(Command):
        max_args = 1
        min_args = 0

        usage = "[Config]"
        summary = "Upgrades the database using sqlalchemy migrations"
        group_name = "SQLAlchemy Migrations"

        parser = Command.standard_parser(verbose=True)
        parser.add_option("-V", "--version",
                          action='store',
                          dest='version',
                          type='int',
                          help="will upgrade to given version instead of latest")

        def command(self):
            if len(self.args) == 1:
                conf_path = self.args[0]
            else:
                conf_path = 'development.ini'

            from paste.deploy import appconfig
            from migrate.versioning.api import upgrade
            from os.path import dirname, abspath
            from pylons import config

            config = appconfig('config:'+abspath(conf_path))
            url = config['sqlalchemy.url']
            #TODO: get app name or the app root path
            #repository = config['here'] + '/{project}' + '/migrations'
            from {project} import migrations

            repository = migrations.__path__[0]

            upgrade(url=url, repository=repository, version=self.options.version)

entrypoint need to be added for the command

**setup.py**

.. code-block:: python

    entry_points="""
    [paste.app_factory]
    main = pharmaretail.config.middleware:make_app

    [paste.app_install]
    main = pylons.util:PylonsInstaller

    [paste.paster_command]
    upgrade = pharmamfg.migrations.upgrade:Upgrade
    """,


Also I changed my websetup to create versioned db

**{project}/websetup.py**

.. code-block:: python

    def setup_app(command, conf, vars):
        """Place any commands to setup pharmaretail here"""
        load_environment(conf.global_conf, conf.local_conf)

        # Create the tables if they don't already exist
        try:
            ControlledSchema.create(elixir.engine,'pharmamfg/migrations/')
        except DatabaseAlreadyControlledError:
            print "Database already under version control"
