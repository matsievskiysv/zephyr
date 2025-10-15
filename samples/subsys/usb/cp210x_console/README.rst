.. zephyr:code-sample:: usb-cp210x-console
   :name: Console over USB CP210x
   :relevant-api: usbd_api uart_interface

   Output "Hello World!" to the console over USB CP210x.

Overview
********

This example application shows how to use the CP210x UART provided by the new
experimental USB device stack as a serial backend for the console.

Requirements
************

This project requires an USB device driver, which is available for multiple
boards supported in Zephyr.
The operating system needs to be configured to bind PID-VID pairs to the
appropriate driver. For example, on Linux, to bind PID 0x2fe3 VID 0x0002
to the cp210x driver, one needs to create a file
file:`/etc/udev/rules.d/99-zephyr-cp210x.rules` with the following lines

.. code-block:: udev

   ACTION=="add", SUBSYSTEM=="usb", ATTRS{idVendor}=="2fe3", ATTRS{idProduct}=="0002", \
   RUN+="/sbin/modprobe cp210x", \
   RUN+="/bin/sh -c 'echo 2fe3 0002 > /sys/bus/usb-serial/drivers/cp210x/new_id'"

Building and Running
********************

This sample can be built for multiple boards, in this example we will build it
for the reel_board board:

.. zephyr-app-commands::
   :zephyr-app: samples/subsys/usb/cp210x_console
   :board: reel_board
   :goals: flash
   :compact:

Plug the board into a host device, for sample, a PC running Linux OS.
The board will be detected as a CP210x serial device. To see the console output
from the sample, use a command similar to :command:`minicom -D /dev/ttyUSB1`.

.. code-block:: console

   Hello World! arm
   Hello World! arm
   Hello World! arm
   Hello World! arm
