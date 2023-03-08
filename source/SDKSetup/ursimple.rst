URSim Quick Start Guide 
=======================
This page will explain how URSim can be spun up.

1. Load URSim image
-------------------

Download the URSim image arnold-ursim-arnold-container-amd64-prod-.tar
(749 MB) and place it in the urcapx-dev workspace.

2. Run URSim container
----------------------

2.1. Run Container
~~~~~~~~~~~~~~~~~~

Let’s run the URSim container inside the urcapx-dev container workspace:

.. code:: bash

   ./runURSim.sh

To see possible arguements type:

.. code:: bash

   ./runURSim.sh --help

A staging folder will be created to hold the created programs,
installations and data from the installedURCaps.

2.2. Stop Container
~~~~~~~~~~~~~~~~~~~

To later stop the URSim container from inside the urcapx-dev, execute
following command:

.. code:: bash

   ./stopURSim.sh

This will stop URSim and remove its container.

3. Access vnc
-------------

Click on the link `vnc <http://localhost:6080/vnc.html>`__ or open the
link manually in browser

.. code:: bash

   http://localhost:6080/vnc.html

4. Install URCap
----------------

Build and install .urcapx files following the guidelines in urcapx-dev
environment. See
`urcapctl-developer-guide <urcapx-dev/docs/urcapctl-developer-guide.md>`__.

5. Restart PolyScope
--------------------

In the PolyScope application select restart to be able to use the newly
installed URCap.
