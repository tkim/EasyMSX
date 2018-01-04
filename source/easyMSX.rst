#######
EasyMSX 
#######

The EasyMSX allows getting orders, routes, and static data from EMSX API service. The EasyMSX allows adding notification handler on the real-time events. There is an observer pattern that can throw exceptions.  

The ``EasyMSXSample`` in C Sharp illustrates how to use ``EasyMSX`` in C Sharp. 

The ``easymsxdemo-1.0.0`` in python illustrates what can be done with ``easymsx`` in python.


EasyMSX C Sharp
===============

For running ``EasyMSX`` in C Sharp, the user needs to reference the following on ``EasyMSXSample`` before building and running the code sample.

* Bloomberg API SDK in CSharp 
* EasyMSX.dll  


The GitHub link to the EasyMSX sample in `C Sharp EasyMSX`_.

.. note::

	Bloomberg API SDK in CSharp ``e.g. c:\blp\DAPI\APIv3\DotnetAPI\v3.8.9.2\lib\Bloomberglp.Blpapi.dll`` 

    EasyMSX.dll ``e.g. c:\... \cs_EasyMSX-master\EasyMSX\bin\Debug\EasyMSX.dll``


.. _C Sharp EasyMSX: https://github.com/tkim/EasyMSXRepository/tree/master/CSharp


EasyMSX Python
==============

The ``easymsx-1.0.0`` inside the Python folder consists of the core code samples for ``easymsx`` in python. The ``easymsxdemo.py`` is the demo script to use for python.


* Please download the ``easymsxdemo`` folder and extract ``easymsxdemo`` into ``easymsx-1.0.0`` folder.

* Change directory to ``easymsx-1.0.0`` and in the directory run the following command:-

.. code-block:: none

	C:\Users\Me\easymsx-1.0.0>C:\Python34\python.exe setup.py install


.. note::
	
	Please make sure the path for python is set to where you currently have your python 3 installed. 


The GitHub link to the EasyMSX sample in `python EasyMSX`_.

.. _python EasyMSX: https://github.com/tkim/EasyMSXRepository/tree/master/Python


