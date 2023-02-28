urcapctl-developer-guide, version 0.2.1 dec 21. 2022 \* 1.
`Prerequisites <#Prerequisites>`__ \* 2. `Add URCap development docker
image to local machine
registry <#AddURCapdevelopmentdockerimagetolocalmachineregistry>`__ \*
3. `VSCode - open project in remote
window <#VSCode-openprojectinremotewindow>`__ \* 4. `Copy urcap
example <#Copyurcapexample>`__ \* 5. `Compile urcap
sample <#Compileurcapsample>`__ \* 6. `Deploy urcap <#Deployurcap>`__ \*
6.1. `Get the IP of the URSim <#GettheIPoftheURSim>`__ \* 6.2.
`Deploy <#Deploy>`__ \* 7. `Hard reset URSIM <#HardresetURSIM>`__

.. raw:: html

   <!-- vscode-markdown-toc-config
       numbering=true
       autoSave=true
       /vscode-markdown-toc-config -->

.. raw:: html

   <!-- /vscode-markdown-toc -->

User guide for URCapX development
=================================

1. Prerequisites
----------------

| This development environment uses Visual Code Dev Containers extension
  to be able to use Visual Studio Code’s full feature set inside a
  container.
| See `Developing inside a
  Container <https://code.visualstudio.com/docs/devcontainers/containers>`__
  for more information about developing inside a docker container.
| The following should be installed before continuing this guide:

1. `Docker <https://www.docker.com/>`__
2. `Visual Studio Code <https://code.visualstudio.com/download>`__

 

2. Add URCap development docker image to local machine registry
---------------------------------------------------------------

1. Manually download the URCap development zip file
   (urcapx-dev.x.x.x.zip) on to local machine from pen drive / cloud
   drive.

2. Unzip the urcapx-dev zip file.

3. Load urcap-dev docker image into registry from inside the
   ‘urcapx-dev’ folder

.. code:: bash

   cd urcapx-dev
   docker load --input <urcap-dev.x.x.x.tar>
   # example:  docker load --input urcap-dev.0.4.10.tar

 

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

 

4. Copy urcap example
---------------------

The sdk is placed in ``/tmp/sdk``

1. Open terminal in vscode ``(Ctrl + j)`` or use the menu. Size it
   according to you needs. ``(Ctrl + j)`` toggles between editor and
   terminal.

.. code:: bash

   pwd  # /workspaces/urcapx-dev
   cp -r /tmp/sdk/samples/swing/com.ur.urcap.examples.dockerdaemon dockerdaemon

you will notice a dockedaemon folder in your workspace.

 

5. Compile urcap sample
-----------------------

Use cli tool ``(urcapctl)`` to build and deploy built urcapx

.. code:: bash

   pwd  # /workspaces/urcapx-dev
   urcapctl build --help
   urcapctl build [urcap_src_dir] [urcapx_dst_dir]
   # example: urcapctl build dockerdaemon .

After this command you should see dockerdaemon.urcapx file in your
destination folder.  

6. Deploy urcap
---------------

You can deploy either directly to a robot, given that you know the robot
ip, or you can deploy it to URSim docker container where UR software
stack is running.

6.1. Get the IP of the URSim
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

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

6.2. Deploy
~~~~~~~~~~~

.. code:: bash

   pwd  # /workspaces/urcapx-dev
   urcapctl deploy --help
   urcapctl deploy [dst_ip_address] [path_to_urcapx]
   # example: urcapctl deploy 172.17.0.2 dockerdaemon.urcapx

If the URCap is already installed they you will get an error response.
saying it is already installed. In order to force replace existing URCap
then use ``--replace`` flag

.. code:: bash

   urcapctl deploy [dst_ip_address] [path_to_urcapx] --replace
   # example: urcapctl deploy 172.17.0.2 dockerdaemon.urcapx --replace

7. Hard reset URSIM
-------------------

If you like to reset ursim, in this case remove all installed urcaps

.. code:: bash

   # stop ursim container
   ./stopURSim.sh
   # remove staging folder. you might need sudo permissions
   sudo rm -rf staging
   # remove container volume
   docker volume rm ursim-dind-var-lib-docker
