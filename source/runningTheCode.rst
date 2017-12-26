################
Running the Code
################

Please see below for the relevant programming languages to run EasyMSX Sample.


######
Python
######


EasyMSX Python
==============

The EasyMSX Python folder consists of the core code samples for EasyMSX in python. The ``EasyMSXSample.py`` is the sample to use for python.

Please run ``EasyMSXSample.py`` inside the EasyMSXPython folder to run the example in python. 

The GitHub link to the EasyMSX sample in `python`_.


RuleMSX Python
===============

The new python RuleMSX runs in Python 3. This particular build was tested with Python 3.4 in windows 10. 

* Create new directory and extract easymsx-1.0.0 and rulemsx-1.0.0 into the new directory.

.. code-block:: none

	C:\Users\Me\_rulemsx>dir
 	Volume in drive C is Windows
 	Volume Serial Number is ABCD-1234

 	Directory of C:\Users\Me\_rulemsx

	12/21/2017  09:08 AM    <DIR>          .
	12/21/2017  09:08 AM    <DIR>          ..
	12/21/2017  09:01 AM    <DIR>          easymsx-1.0.0
	12/21/2017  09:01 AM    <DIR>          rulemsx-1.0.0
	12/21/2017  09:01 AM    <DIR>          RuleMSXDemo.py
	               1 File(s)              0 bytes
	               4 Dir(s)  11,538,878,464 bytes free


* Change directory to rulemsx-1.0.0 and in the directory run the following command:-

.. code-block:: none

	C:\Users\Me\_rulemsx>cd rulemsx-1.0.0

	C:\Users\Me\_rulemsx\rulemsx-1.0.0>C:\Python34\python.exe setup.py install


.. note::
	
	Please make sure the path for python is set to where you currently have your python 3 installed.


* Change directory to easymsx-1.0.0 and in the diretory run the following command:-

.. code-block:: none
	
	C:\Users\Me\_rulemsx>cd easymsx-1.0.0

	C:\Users\Me\_rulemsx\easymsx-1.0.0>C:\Python34\python.exe setup.py install

*  Run RuleMSXDemo.py

.. code-block:: none
	
	C:\Users\Me\_rulemsx>py -3 RuleMSXDemo.py
	Initialising RuleMSX...
	RuleMSX initialised...
	Initialising EasyMSX...
	EasyMSX initialised...
	Create RuleSet...
	Building Rules...
	Rules built.
	RuleSet ready...
	Press any to terminate

	
The link to the `python RuleMSX`_.


#######
C Sharp
#######

EasyMSX C Sharp
===============

The EasyMSX in C Sharp works similarly as EasyMSXpython. For running EasyMSX in C Sharp, the user needs to reference the following on EasyMSXSample before building and running the code sample.

* Bloomberg API SDK in CSharp 
* EasyMSX.dll  


The GitHub link to the EasyMSX sample in `C Sharp`_.

.. note::

	Bloomberg API SDK in CSharp ``e.g. c:\blp\DAPI\APIv3\DotnetAPI\v3.8.9.2\lib\Bloomberglp.Blpapi.dll`` 

    EasyMSX.dll ``e.g. c:\... \cs_EasyMSX-master\EasyMSX\bin\Debug\EasyMSX.dll``


EasyMKT C Sharp
===============

The EasyMKT and EasyMKTSample are currently available only in C Sharp. For running EasyMKT in C Sharp, the user needs to reference the following on EasyMKTSample before building and running the code sample.

* Bloomberg API SDK in CSharp
* EasyMKT.dll 


.. note::

	Bloomberg API SDK in CSharp ``e.g. c:\blp\DAPI\APIv3\DotnetAPI\v3.8.9.2\lib\Bloomberglp.Blpapi.dll``

	EasyMKT.dll ``e.g. c:\... \cs_EasyMKT-master\EasyMKT\bin\Debug\EasyMKT.dll``



RuleMSX C Sharp
===============

 For running RuleMSX in C Sharp, the user needs to reference the following on RuleMSXSample before building and running the code sample.

* Bloomberg API SDK in CSharp 
* EasyMKT.dll  
* EasyMSX.dll 
* RuleMSX.dll

.. note::

	Bloomberg API SDK in CSharp ``e.g. c:\blp\DAPI\APIv3\DotnetAPI\v3.8.9.2\lib\Bloomberglp.Blpapi.dll``

	EasyMKT.dll ``e.g. c:\... \cs_EasyMKT-master\EasyMKT\bin\Debug\EasyMKT.dll``

	EasyMSX.dll ``e.g. c:\... \cs_EasyMSX-master\EasyMSX\bin\Debug\EasyMSX.dll``

	RuleMSX.dll ``e.g. c:\... \cs_RuleMSX-master\RuleMSX\bin\Debug\RuleMSX.dll`` 



Full EasyMSX Code Samples
=========================

The link to the main `EasyMSX Code Sample`_.


Full EMSX API Documentation 
===========================

The link to the main `EMSX API Documentation`_.


Full EMSX API Code Samples
==========================

The github link to the `EMSX API Code Sample`_. 



.. _python: https://github.com/tkim/EasyMSXRepository/tree/master/Python

.. _C Sharp: https://github.com/tkim/EasyMSXRepository/tree/master/CSharp


.. _python RuleMSX: https://github.com/tkim/EasyMSXRepository/tree/master/Python

.. _EasyMSX Code Sample: https://github.com/tkim/EasyMSXRepository


.. _EMSX API Documentation: http://emsx-api-doc.readthedocs.io/en/latest/

.. _EMSX API Code Sample: https://github.com/tkim/emsx_api_repository
