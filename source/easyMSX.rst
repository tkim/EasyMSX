#######
EasyMSX 
#######

The EMSX API is just another service in Bloomberg API V3.  The Bloomberg API follows an event-driven asynchronous API paradigm. 

The Bloomberg API is lightweight, thread safe and maintains extensible service-oriented data model. The Bloomberg API generally understands the concept of subscription and request-response services.

The EasyMSX allows getting orders, routes, and static data from EMSX API service. The EasyMSX allows adding notification handler on the real-time events. There is an observer pattern that can throw exceptions.  


EasyMSXTest
===========

The EasyMSXTest is a sample application to test EasyMSX to extract the delta's from EMSX API Order and Route subscription service.


EasyMSX C Sharp
===============

The EasyMSX in C Sharp works similarly as EasyMSXpython. For running EasyMSX in C Sharp, the user needs to reference the following on EasyMSXSample before building and running the code sample.

* Bloomberg API SDK in CSharp 
* EasyMSX.dll  


The GitHub link to the EasyMSX sample in `c sharp EasyMSX`_.

.. note::

	Bloomberg API SDK in CSharp ``e.g. c:\blp\DAPI\APIv3\DotnetAPI\v3.8.9.2\lib\Bloomberglp.Blpapi.dll`` 

    EasyMSX.dll ``e.g. c:\... \cs_EasyMSX-master\EasyMSX\bin\Debug\EasyMSX.dll``


.. _c sharp EasyMSX: https://github.com/tkim/EasyMSXRepository/tree/master/CSharp


EasyMSX Python
==============

The EasyMSX Python folder consists of the core code samples for EasyMSX in python. The ``EasyMSXSample.py`` is the sample to use for python.

Please run ``EasyMSXSample.py`` inside the EasyMSXPython folder to run the example in python. 

The GitHub link to the EasyMSX sample in `python EasyMSX`_.

.. _python EasyMSX: https://github.com/tkim/EasyMSXRepository/tree/master/Python


