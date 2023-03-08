Compile and Deploy URCap Example 
================================

Now that your dev environment has been set up, you can start using the new features of our SDK.  
There have been major changes to the way URCaps are structured, compiled, and deployed to the robot or URSim. 
This section will walk you through building your first URCap on PolyScope 6, with a prewritten example that implements the different structure. 

DockerDaemon Example
--------------------
#. Copy the example project by running 

.. code:: bash

    cp -r /tmp/sdk/samples/swing/com.ur.urcap.examples.dockerdaemon dockerdaemon

The **dockerdaemon** folder should now be in the /workspaces/urcapx-dev directory. 
#. Compile the URCap with the UR CLI tool by running 

.. code:: bash

    urcapctl build [urcapx_src_dir] [urcapx_dst_dir]

