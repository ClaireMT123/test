
.. _hardware-connection-label:

Hardware Connection
=======================


The Camport SDK needs to be used in conjunction with the Percipio depth camera. The Camport SDK supports all models of Percipio depth cameras currently on sale. For details on the models and specifications of Percipio depth cameras, see :ref:`Product Specifications <camera-param-label>`.

This section mainly introduces the connection methods between the camera and the computer.

For details on the power supply method of the camera, see the details page of each camera in :ref:`Product Specifications <camera-param-label>` .

Some cameras support triggering by an external signal. For details about this, see :ref:`External Trigger <external-trigger-label>`.

.. important::

    For safety precautions to be taken before hardware connection, see :doc:`Safety Statement </COPYRIGHTS>`.


.. _net-connection-label:

Depth Camera over Ethernet
------------------------------


Percipio depth cameras over Ethernet need to be powered by an external power supply, and some camera models also support POE power supply. By default, the depth camera uses DHCP to dynamically obtain an IP address from the server.

Before connecting the camera to the computer, please make sure that the computer's network card is set to automatic IP address assignment mode (DHCP).



**Method I for Connecting to Ethernet**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Connect the camera directly to the computer's gigabit Ethernet interface via a gigabit Ethernet cable.

After powered on for about 1 minute, the camera can successfully negotiate with the computer and obtain an IP address in the 169.254.xx.xx network segment.

Use the SDK sample program ListDevices to enumerate devices. If the IP address and the serial number of the camera are successfully enumerated, run SimpleView_FetchFrame.exe -id <device ID> to view images. The device ID (i.e., the serial number) can be obtained from the device label or from the enumeration results.

.. figure:: ../image/netcon-en.png
    :width: 540px
    :align: center
    :alt: Method I for Connecting to Ethernet
    :figclass: align-center

    Method I for Connecting to Ethernet


**Method II for Connecting to Ethernet**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Connect the camera and the computer to the same Gigabit Ethernet switch via Gigabit Ethernet cables.

After powered on for about 1 minute, the camera can successfully negotiate with the computer and obtain IP addresses in the 169.254.xx.xx network segment.

Use the SDK sample program ListDevices to enumerate devices. If the IP address and the serial number of the camera are successfully enumerated, run SimpleView_FetchFrame.exe -id <device ID> to view images. The device ID (i.e., the serial number) can be obtained from the device label or from the enumeration results.

.. figure:: ../image/netswitch-en.png
    :width: 540px
    :align: center
    :alt: Method II for Connecting to Ethernet
    :figclass: align-center

    Method II for Connecting to Ethernet


**Method III for Connecting to Ethernet**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Connect the camera and the computer to the same Gigabit Ethernet switch via Gigabit Ethernet cables, and connect the switch to a router that supports DHCP service function or enable a DHCP server within the LAN.

After powered on for about 1 minute, the camera can successfully negotiate with the computer and obtain IP addresses in the 169.254.xx.xx network segment.

Use the SDK sample program ListDevices to enumerate devices. If the IP address and the serial number of the camera are successfully enumerated, run SimpleView_FetchFrame.exe -id <device ID> to view images. The device ID (i.e., the serial number) can be obtained from the device label or from the enumeration results.

.. figure:: ../image/netroute-en.png
    :width: 540px
    :align: center
    :alt: Method III for Connecting to Ethernet
    :figclass: align-center

    Method III for Connecting to Ethernet


.. note::

   If the camera cannot be enumerated or if the camera's IP address needs to be modified, see :ref:`Application Example-Setting the IP address of the depth camera over Ethernet <application1-label>`.


