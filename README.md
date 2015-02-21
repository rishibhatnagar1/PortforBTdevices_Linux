# PortforBTdevices_Linux
Hello everyone. If you are a new linux user and you have shifted from Windows , I am guessing you have already experienced the issue with connecting devices using Bluetooth and USB , while working with Arduino or Processing. Windows assigns something known as 'COM' ports to all the devices connected to the system using USB or otherwise. While interfacing them and using them with Processing or Arduino , one can directly select the 'COM' port and start coding. In the case of Linux however , you have to create and assign port numbers to the devices (specially in the case of Blue Tooth devices) . To start with , if you have installed arduino , to check the port number where the arduino board is connected , press Cntrl+ Alt+t to open terminal . This has a unix base. Type the following command : dmesg

This should give you the name of the port number that has been assigned to the board.

Apologies for the weird cropping. Anyways , The port number in my case is assigned for Arduino Uno and it is given by 'ttyACM0': USB ACM device. The same command should work in all the linux system.

For the case of Bluetooth Devices , there is a different method that needs to be followed. Type in the following commands in the Terminal Window :

sudo hcitool scan ## This essentially scans the bluetooth devices

The response to it should look something like this : Scanning ... 00:02:C0:7A:F5:17 BlueGPS 7AC517

The number is 00:02:C0:7A:F5:17 is the address of the bluetooth device. You now need to assign it to a port number.

Use the following commands :

sudo rfcomm bind /dev/rfcomm0 00:02:C7:7D:F5:17 1

ls -l /dev/rfcomm0

The terminal returns the following message :

crw-rw---- 1 root dialout 216, 0 2014-07-16 20:03 /dev/rfcomm0

Congratulations ,you have just created your own port number. It in this case is /dev/rfcomm0. Similarly , you can create port number for multiple BT devices.

Credits : http://www.westernwillow.com/cms/blog/franco/creating-bluetooth-serial-port-ubuntu
