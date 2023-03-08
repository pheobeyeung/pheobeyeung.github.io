Software Requirements and Set Up
================================

*Prerequisites:* *You must
have*\ `Git <https://git-scm.com/downloads>`__\ *,*\ `Visual Studio
Code <https://code.visualstudio.com/download>`__\ *,
and*\ `Docker <https://www.docker.com/products/docker-desktop/>`__\ *installed
and configured.*

Docker
------

VSCode
------
If you are using Windows, you need to perform these steps before
proceeding: 1. Open Git Bash from the Start menu as adminstrator. 2. Run
``git config --system core.longpaths true`` in the terminal. 3. Ensure
that your wsl engine is installed correctly and up to date.


1. Open Docker Desktop to ensure that the program is running.
2. Install the `Remote Development extension
   pack <https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack>`__
   for Visual Studio Code.
3. Open Visual Studio Code.
4. Type ``Ctrl+Shift+G`` to open source control. It should also be the
   third icon from the top on the left side of the screen.
5. Enter ``https://github.com/pheobeyeung/universal_robots_sdk`` as the
   remote repository to clone, and pick a desired location to save onto
   your drive.
6. Open the cloned repository in VSCode, and reopen in Dev container
   when prompted. This may take several minutes to load. *6a. If the
   prompt does not automatically pop up, you can reopen the folder in a
   dev container by accessing the command palette through:*

   -  ``Ctrl+Shift+P`` *on Windows/Linux*
   -  ``Command+Shift+P`` *on Mac* *and search for* **Dev Containers:
      Reopen in Container**

7. Type :literal:`Ctrl+`+Shift` to open the Terminal. Congrats! The SDK
   environment is now successfully setup! 
