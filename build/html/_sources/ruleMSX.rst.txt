#######
RuleMSX 
#######

The RuleMSX is designed to use the rete algorithm to create an efficient business rule management system to work with Bloomberg EMSX API for automated trade execution for equities, futures, and options.

The RuleMSX views each rule exists as a stand-alone rule that is either true or false at any given moment. 

A pattern contains one or more rules. All the rules in a pattern must evaluate to true for the action attached to the pattern to be executed. In this case, the action itself is responsible for introducing the new rules to be checked and/or new patterns or patterns to be removed from the set. 

RETE Algorithm
==============

The word rete is Latin for net or network. 
The rete algorithm is essentially a pattern matching algorithm. 

The main objective behind rete algorithm for RuleMSX is to decouple the various trading or business rules from rule execution or executing sequences on a particular data set. 

The data set here can be both trading data obtained from EMSX API, market data, or non-trading based proprietary data set.


Earlier Version
===============

The initial approach to RuleMSX handled the rete in the following structure where each RuleSet consists of a single rule. Each rule consisted of child rules and rule evaluator.


.. image:: /image/rete_orig.png


As part of the reiteration of RuleMSX, we have made the changes to reflect the rete algorithm in the following structure: 


.. image:: /image/rete_new.png


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


The link to the `c sharp RuleMSX`_.

.. _c sharp RuleMSX: https://github.com/tkim/EasyMSXRepository/tree/master/CSharp


RuleMSX Python
==============

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

.. _python RuleMSX: https://github.com/tkim/EasyMSXRepository/tree/master/Python



