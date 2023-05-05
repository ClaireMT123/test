

.. _application-reference-label:

SDK Application Reference 
------------------------------

Some simple applications can be realized by running the executable files in the ``lib/win/hostapp/x64`` directory of the SDK, or running the executable files in the ``sample/build/bin/Release`` directory you compiled.

In addition, Percipio provides an image viewing software called **Percipio Viewer**, which is developed based on Camport SDK. It allows users to quickly view depth images, color images, infrared images, and point clouds. It also provides online adjustments for camera parameters, such as exposure parameters and laser power. The download link for the **Percipio Viewer** installation package is  https://www.percipio.xyz/downloadcenter/. For instructions on how to use Percipio Viewer, see :doc:`Percipio Viewer User Guide </viewer_en>`.

.. _sample-exe-label:
          
Descriptions of the Sample Programs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
  
ListDevices
  This sample program is used to enumerate all depth cameras connected to the host computer.
  

DumpAllFeatures
  This sample program is used to enumerate the various components of the depth camera and their features. It is also used to enumerate the read and write permissions information supported for each feature.

ForceDeviceIP   
  This sample program is used to set the IP address of the depth camera over Ethernet.
  

LoopDetect  
  This sample program is used to handle data communication exceptions caused by environmental instability and other factors.
  
  
SimpleView_FetchFrame 
  This sample program is used to set the depth camera to free acquisition mode, in which it continuously captures images and outputs image data at the highest frame rate.

SimpleView_Callback  
  This sample program is used to set the depth camera to free acquisition mode, in which it continuously captures images, and at the same time performs OpenCV rendering in an independent data processing thread (to avoid blocking the image data acquisition process) and outputs image data.

  
SimpleView_FetchHisto  
  This sample program is used to obtain image brightness histograms.

SimpleView_MultiDevice 
  This sample program is used to enable multiple depth cameras to capture images simultaneously and continuously.
  
SimpleView_Point3D  
  This sample program is used to obtain 3D point cloud data.
  
SimpleView_Registration 
  This sample program is used to obtain the camera's intrinsic and extrinsic parameters, depth images, and color images, and is used to align the depth images and color images.
  
SimpleView_TriggerDelay
  This sample program is used to set the delay time for hardware trigger. The depth camera waits for a specific delay time after receiving a hardware trigger signal, and then capture images.

SimpleView_TriggerMode0
  This sample program is used to set the depth camera to work in mode 0, where the camera continuously captures images and outputs image data at the highest frame rate.

SimpleView_TriggerMode1
  This sample program is used to set the depth camera to work in mode 1, where the camera captures images and outputs image data after receiving a software trigger command or a hardware trigger signal.

SimpleView_TriggerMode_M2S1
  This sample program is used to set the master device (camera) to work in mode 2, and multiple slave devices (cameras) to work in mode 1, so as to achieve cascade triggering of multiple depth cameras and simultaneous image acquisition.

  After receiving a software trigger command sent from the host computer, the master device outputs a hardware trigger signal through the hardware TRIG_OUT pin, while at the same time triggering its own image acquisition and outputing depth images. After receiving the hardware trigger signal from the master device, the slave devices capture images and output depth images.



SimpleView_TriggerMode_M3S1
  This sample program is used to set the master device (camera) to work in mode 3, and multiple slave devices (cameras) to work in mode 1, so as to achieve cascaded triggering of multiple depth cameras according to the set frame rate and simultaneous image acquisition.

  The master device outputs a hardware trigger signal through the hardware TRIG_OUT interface according to the set frame rate, while at the same time triggering its own image acquisition and outputing depth images. After receiving the hardware trigger signal from the master device, the slave devices capture images and output depth images.



SimpleView_TriggerMode18
  This sample program is used to set the depth camera to work in mode 18. After receiving a software trigger command or a hardware trigger signal, the camera captures one round of images according to the set frame rate in a "1+duty" manner and outputs image data (1: emits one time of (floodlight); duty: emits "duty" times of laser light).

SimpleView_TriggerMode19
  This sample program is used to set the depth camera to work in mode 19. After receiving a software trigger command or a hardware trigger signal, the camera continuously captures images in a "1+duty" manner and outputs image data (1: emits one time of (floodlight); duty: emits "duty" times of laser light).

SimpleView_TriggerMode20
  This sample program is used to set the depth camera to work in mode 20. Based on the set trigger start time (start_time_us), time interval array between every two frames (offset_us_list[]) and the trigger count (offset_us_count), the camera captures and outputs (1 + offset_us_count) frames of images at the set time intervals. Before enabling this mode, make sure the camera PTP synchronization is activated and offset_us_count is not larger than 50.



SimpleView_TriggerMode21
  This sample program is used to set the depth camera to work in mode 21. Based on the set trigger start time (start_time_us), trigger count (trigger_count), and trigger time interval (peroid_us), the camera captures and outputs one frame of image each time at a time interval assigned by "peroid_us". Before enabling this mode, make sure PTP synchronization is activated for the camera.



.. _application1-label:

Application Example: Setting the IP Address for a Depth Camera over Ethernet
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The sample program for setting the IP address for a depth camera over Ethernet is ForceDeviceIP.

**Instructions**

* Setting a temporary IP address:

  Command: ForceDeviceIP.exe -force <MAC> <newIP> <newNetmask> <newGateway>

  Where <MAC> can be obtained from the device label, typically in the format of xx:xx:xx:xx:xx:xx, <newIP> is the specified IP address, and <newNetmask> and <newGateway> are set according to newIP. After executing this command, the IP address of the depth camera over Ethernet will be modified to the IP address specified by the command. The modification will take effect immediately. After power-off and reboot, the IP configuration of the camera will restore to its original one.
  
  Example: ForceDeviceIP.exe -force 68:f7:56:36:90:a3 192.168.1.160 255.255.255.0 192.168.1.1


* Setting a static IP address:

  Command: ForceDeviceIP.exe -static <MAC> <newIP> <newNetmask> <newGateway>

  Where <MAC> can be obtained from the device label, typically in the format of xx:xx:xx:xx:xx:xx, <newIP> is the specified IP address, and <newNetmask> and <newGateway> are set according to newIP. After executing this command, the IP address of the depth camera over Ethernet will be modified to the IP address specified by the command. The modification will take effect immediately. After power-off and reboot, the IP configuration of the camera will maintain the one configured by the command.

  Example: ForceDeviceIP.exe -static 68:f7:56:36:90:a3 192.168.1.160 255.255.255.0 192.168.1.1


* Setting a dynamic IP address (supported by new camera models only):

  Command: ForceDeviceIP.exe -dynamic <MAC> 

  Where <MAC> can be obtained from the device label, usually in the format of xx:xx:xx:xx:xx:xx. After executing this command, the IP configuration of the depth camera over Ethernet will be cleared and restored to DHCP dynamic IP acquisition mode immediately. After power-off and reboot, the camera will actively request an IP address via DHCP. This command is not supported by some old camera models.

  Example: ForceDeviceIP.exe -dynamic 68:f7:56:36:90:a3


* Set to dynamic IP address (supported by both old and new camera models)

  Command: ForceDeviceIP.exe -dynamic <MAC> <newIP> <newNetmask> <newGateway>

  Where <MAC> can be obtained from the device label, usually in the format of xx:xx:xx:xx:xx:xx, and <newIP> , <newNetmask> and <newGateway> are temporary IP address and subnet mask. After executing this command, the newIP configuration will be temporarily used. The IP configuration of the depth camera over Ethernet will be cleared and restored to DHCP dynamic IP acquisition mode to immediately obtain a dynamic IP address. After power-off and reboot, the camera will maintain to request an IP address via DHCP.

  Example: ForceDeviceIP.exe -dynamic 68:f7:56:36:90:a3 192.168.1.160 255.255.255.0 192.168.1.1


**Application scenario 1**

If the Percipio depth camera over Ethernet cannot be enumerated through the SDK sample program ListDevices, do the following (taking Windows 10 platform as an example): 

1. Execute the command ForceDeviceIP.exe -force <MAC> <newIP> <Netmask> <Gateway> under the SDK sample/build/bin/Release directory. The newly set newIP should be on the same network segment as the computer's IP address, and the subnet mask and gateway should be consistent with the computer.

2. Execute the following command as needed to set the camera's IP address to:

   - Dynamic IP address: ForceDeviceIP.exe -dynamic <MAC> or ForceDeviceIP.exe -dynamic <MAC> <newIP> <newNetmask> <newGateway>
   
   - Static IP address: ForceDeviceIP.exe -static <MAC> <newIP> <newNetmask> <newGateway>



**Application scenario 2**
If you want to change the dynamic IP address of the Percipio network depth camera to a static IP address, do the following (taking Windows 10 platform as an example): 

1. If the newly modified static IP address is not on the same network segment as the computer's IP address, modify the computer's IP address first.

   For example: If the newly modified static IP address is 192.168.0.XX, open the Control Panel on your computer, select "Network and Internet" > "Network and Sharing Center" > "Change adapter settings" > "Ethernet" > "Internet Protocol Version 4 (TCP/IPv4)", select "Use the Following IP Address" in the dialog box **Internet Protocol Version 4 (TCP/IPv4) Properties**, and set the IP address, subnet mask, and gateway:
   
   .. figure:: ../image/modify-pc-ip-en.png
      :width: 500px
      :align: center
      :alt: Modyfying the Computer's IP Address
      :figclass: align-center

      Modyfying the Computer's IP Address

2. Enter the sample/build/bin/Release directory in the SDK and execute the command: ForceDeviceIP.exe -static <MAC> <newIP> <Netmask> <Gateway>, where newIP is the static IP address that needs to be set to.

