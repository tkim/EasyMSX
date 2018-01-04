#######
EasyMKT 
#######

The EasyMKT and EasyMKTSample demonstrate one possible way to build caching data on Bloomberg real-time market data.

The ``EasyMKTSample`` in C Sharp illustrates how to use ``EasyMSX`` in C Sharp.

The ``easymktdemo-1.0.0`` in python illustrates what can be done with ``easymkt`` in python. 

EasyMKT C Sharp
===============

For running ``EasyMKT`` in C Sharp, the user needs to reference the following on ``EasyMKTSample`` before building and running the code sample.

* Bloomberg API SDK in CSharp
* EasyMKT.dll 

The Github link to the EasyMKT in `C Sharp EasyMKT`_.

.. note::

	Bloomberg API SDK in CSharp ``e.g. c:\blp\DAPI\APIv3\DotnetAPI\v3.8.9.2\lib\Bloomberglp.Blpapi.dll``

	EasyMKT.dll ``e.g. c:\... \cs_EasyMKT-master\EasyMKT\bin\Debug\EasyMKT.dll``
 

.. _C Sharp EasyMKT: https://github.com/tkim/EasyMSXRepository/tree/master/CSharp


EasyMKT Python
==============

The ``easymkt-1.0.0`` inside the Python folder consists of the core code samples for ``easymkt`` in python. The ``easymktdemo.py`` is the demo script to use for python.


* Please download the ``easymktdemo`` folder and extract ``easymktdemo`` into ``easymkt-1.0.0`` folder.

* Change directory to ``easymkt-1.0.0`` and in the directory run the following command:-

.. code-block:: none

	C:\Users\Me\easymkt-1.0.0>C:\Python34\python.exe setup.py install


.. note::
	
	Please make sure the path for python is set to where you currently have your python 3 installed. 


The GitHub link to the EasyMKT sample in `python EasyMKT`_.

.. _python EasyMKT: https://github.com/tkim/EasyMSXRepository/tree/master/Python


