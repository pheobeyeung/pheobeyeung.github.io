SDK Installation and Set Up
===========================

1. Manually download the URCap development zip file
   (urcapx-dev.x.x.x.zip) on to local machine from pen drive / cloud
   drive.

2. Unzip the urcapx-dev zip file.

3. Load urcap-dev docker image into registry from inside the
   ``urcapx-dev`` folder

.. code:: bash

   cd urcapx-dev
   docker load --input <urcap-dev.x.x.x.tar>
   # example:  docker load --input urcap-dev.1.0.4.tar

3. VSCode - open project in remote window
-----------------------------------------

1. Open the project in vscode by typing (inside the ‘urcapx-dev’
   folder):

.. code:: bash

   code .

2. Install docker plugin (If not already installed. you will have a
   popup on bottom right corner)
3. Open project in remote window ``(Ctrl + Shift + P)`` –> “Dev
   Containers: Open Folder in Container…”)

 

4. Create a new URCapX
----------------------

In the workspace folder type:

.. code:: bash

   urcapctl create

You will be prompted for Vendor Name, Vendor Id, URCap Name, URCap Id
and what to create. The new URCapX source will be created in a folder
with the same name as the URCap Id.

It is also possible to create a new URCapX without being prompted, but
this requires all the information to be entered as arguments.

To see all available arguments type:

.. code:: bash

   urcapctl create --help
   # example: urcapctl create --vendorId=myvendor --urcapId=myurcap --osgi=myosgibundle --urcapApiVersion=1.13.0 --programNode=MyPrgNode

| The example will create the source code for a new URCapX with id
  ``myurcap``.
| It will include an OSGi bundle called ``myosgibundle`` and a program
  node called ``MyPrgNode``.

5. Add to an existing URCapX
----------------------------

In the workspace folder type:

.. code:: bash

   urcapctl add

You will be prompted for existing URCap Id and what to add. Note that
the URCapX source must be located in the workspace in a folder with same
name as its URCap Id.

It is also possible to add to an existing URCapX source without being
prompted, but this requires all the information to be entered as
arguments.

To see all available arguments type:

.. code:: bash

   urcapctl add --help
   # example: urcapctl add --urcapId=myurcap --installationNode=MyInstNode

The example will add an installation node called ``MyInstNode`` to the
existing URCapX source with id ``myurcap``.

Note that it is also possible to run ``urcapctl add`` from inside an
existing URCapX source folder where the ``manifest.yaml`` is located,
then the URCap Id is not needed as an argument.

6. Copy URCap sample
--------------------

The sdk is placed in ``/tmp/sdk``

1. Open terminal in vscode ``(Ctrl + j)`` or use the menu. Size it
   according to you needs. ``(Ctrl + j)`` toggles between editor and
   terminal.

.. code:: bash

   pwd  # /workspaces/urcapx-dev
   cp -r /tmp/sdk/samples/swing/com.ur.urcap.examples.helloworldswing helloworldswing-osgi

you will notice a ``helloworldswing-osgi`` folder in your workspace.

 

7. Copy URCapX sample containing a container
--------------------------------------------

The sdk is placed in ``/tmp/sdk``

1. Open terminal in vscode ``(Ctrl + j)`` or use the menu. Size it
   according to you needs. ``(Ctrl + j)`` toggles between editor and
   terminal.

.. code:: bash

   pwd  # /workspaces/urcapx-dev
   cp -r /tmp/sdk/samples/swing/com.ur.urcap.examples.dockerdaemon dockerdaemon

you will notice a ``dockerdaemon`` folder in your workspace.

 

8. Convert URCap to URCapX example
----------------------------------

URCaps in the old format can be converted into the new URCapX format
using the ``convert`` command, if the source code is available. Note
that if the URCap contains daemons then the daemons will have to be
added manually after the conversion.

.. code:: bash

   pwd  # /workspaces/urcapx-dev
   urcapctl convert --help
   urcapctl convert [path_to_urcap_source] [path_to_new_urcapx_source]
   # example: urcapctl convert helloworldswing-osgi helloworldswing

Note that the ``--replace`` option can be added if the conversion needs
to be rerun. This will remove the ``[path_to_new_urcapx_source]`` folder
before creating it.

| The convert command will create the ``[path_to_new_urcapx_source]``
  folder with the ``[path_to_urcap_source]`` as a sub-folder, then the
  ``[path_to_urcap_source]/src`` folder will be copied over into the
  ``[path_to_new_urcapx_source]/[path_to_urcap_source]/src`` folder.
| The ``pom.xml`` will be copied over, but with the ``assembly`` and the
  ``profiles`` sections removed. Note that if the java version is 6 then
  it will be upgraded to version 8.
| The ``manifest.yaml`` file will be created from the information in the
  ``pom.xml``, so it may need to be edited.
| An empty ``LICENSE`` file will also be created in the
  ``[path_to_new_urcapx_source]`` folder.

 

9. Compile urcap sample
-----------------------

Use cli tool ``(urcapctl)`` to build and deploy built urcapx

.. code:: bash

   pwd  # /workspaces/urcapx-dev
   urcapctl build --help
   urcapctl build [urcapx_src_dir] [urcapx_dst_dir]
   # example: urcapctl build dockerdaemon .
   # or
   # example: urcapctl build helloworldswing .

After this command you should see dockerdaemon.urcapx file in your
destination folder.

 

10. Deploy urcap
----------------

You can deploy either directly to a robot, given that you know the robot
ip, or you can deploy it to URSim docker container where UR software
stack is running.

10.1. Get the IP of the URSim
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you would like to deploy to URSim, use the URSim IP shown when
running URSim using bash script:

.. code:: bash

   ./runURSim.sh

or get the IP address from the URSim instance running in the Docker
container

.. code:: bash

   docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' <ursim_container_name_or_id>

You can also directly deploy to a physical robot, given that you know
the robot IP address.

10.2. Deploy
~~~~~~~~~~~~

.. code:: bash

   pwd  # /workspaces/urcapx-dev
   urcapctl deploy --help
   urcapctl deploy [dst_ip_address] [path_to_urcapx]
   # example: urcapctl deploy 172.17.0.3 dockerdaemon-v1.0.urcapx

If the URCap is already installed they you will get an error response.
saying it is already installed. In order to force replace existing URCap
then use ``--replace`` flag

.. code:: bash

   urcapctl deploy [dst_ip_address] [path_to_urcapx] --replace
   # example: urcapctl deploy 172.17.0.3 dockerdaemon-v1.0.urcapx --replace

 

11. Hard reset URSim
--------------------

If you like to reset ursim, in this case remove all installed urcaps

.. code:: bash

   # stop ursim container
   ./stopURSim.sh
   # remove staging folder. you might need sudo permissions
   sudo rm -rf staging
   # remove container volume
   docker volume rm ursim-dind-var-lib-docker
