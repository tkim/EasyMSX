#######
RuleMSX 
#######

RuleMSX provides the core functionality of a rule engine. It is designed to inter-operate with the ``EasyMSX`` and ``EasyMKT`` which use the Bloomberg API to access Bloomberg EMSX and market data. The RuleMSX is designed to use the rete algorithm to create an efficient business rule management system to work with Bloomberg EMSX API for automated trade execution for equities, futures, and options.

This functionality is provided in the shape of ``RuleSets``, ``DataSets`` and ``Actions``. By defining Rules and the conditions that must exist for these Rules to be triggered, the user can build complex reasoning based on the content of a DataSet, and how that DataSet changes over time. The Actions are the tasks performed as a result of a Rule being triggered.


RuleSets
========

RuleSets are named entities that represent a collection of RuleSet objects. This is only used to organize rules into logical groupings. A RuleSet is a named collection of Rules. 

An example of a RuleSet would be to route new orders to a particular broker code, based on certain criteria, such as the exchange. We will call this the “AutoRoute” ruleset.

Once we have a RuleSet and a DataSet object, we can execute the RuleSet. RuleSets need one or more supporting DataSets to operate against.


Rules
=====

Each Rule in a RuleSet is a named collection of RuleConditions and RuleActions. When all conditions in a Rule evaluate to True, the associated actions are executed. 

Following the above example, and single rule within the AutoRoute ruleset would be ``RouteUStoBB``, which would route any orders on the ``US`` exchange code to the broker known as ``BB``. The other rule example could be ``RouteLNtoBMTB``.


RuleConditions
==============

A ``RuleCondition`` is a named item within a Rule, which evaluates to either True or False. It does this through client-side code using a ``RuleEvaluator``. A single Rule can have multiple ``RuleConditions``, and they must all evaluate to True for the associated ``RuleActions`` to be executed.

For our ``RouteUStoBB`` example, we would have a condition called ``MustBeUSExchange`` that checked the order to ensure that it was for the ``US`` exchange. Another condition would be that the order must be in a ``NEW`` state, perhaps called ``CheckNEWState``, to ensure that this rule is only triggered once.


RuleEvaluator
=============

A ``RuleEvaluator`` is an abstract class that must be implemented in the client-side code. This abstract class has an ``Evaluate`` method that must be overridden. This method must return ``True`` or ``False``. When the Evaluate method is called, it is passed the current DataSet as a
parameter, to support the determination of the return value.

The abstract class also provides a mechanism for creating a dependency between a Rule and named DataPoints. To do this, we call the ``AddDependantDataPointName`` method of the class, as follows :-

.. code-block:: none

	this.AddDependantDataPointName("OrderStatus")

In this case, we are saying that this particular Rule uses the value of the ``OrderStatus`` ``DataPoint``. The purpose of using this mechanism is to ensure that if the value of ``OrderStatus`` in any ``DataSet`` changes, any ``WorkingRules`` add queue to be re-tested in the next cycle. The change to the value of a ``DataPoint`` is indicated by calling the ``SetStale`` method (see ``DataPointSource``).


RuleActions
===========

A Rule can have many ``RuleActions``. Each ``RuleAction`` has a client-side component called an``ActionExecutor``. When a Rule evaluates to True, all associated ``RuleActions`` are executed.

For example, we would have a ``RuleAction`` called ``RouteOrdertoBB``. which would be called as a consequence of the ``RouteUStoBB`` rules all evaluating to True.


ActionExecutors
===============

An ``ActionExecutor`` is the client-side code that is run when an Action is executed. It is an abstract class that contains an Execute method that must be overridden.

When the ``RouteOrdertoBB`` action is executed, the Execute method of the instance of the abstract class would be called. This is the code that would create and send the route to the broker. Just as with the ``RuleCondition`` evaluators, the executors are passed the current dataset as a parameter when they are called.

DataSets
========

``DataSets`` are named entities that represent a collection of ``DataPoint`` objects. They are only used to organize ``DataPoints`` into logical groupings.

In our current example, we would create a ``DataSet`` object for each order. Once the ``DataSet`` object is defined, we can add it to the list of ``DataSets`` being run through a ``RuleSet`` by the ``ExecutionAgent``.


DataPoints
==========

A ``DataPoint`` is an object that represents a single piece of data. Fundamentally, it is a simple key-value pair. A ``DataPoint`` doesn’t have value itself, but rather has an underlying ``DataPointSource`` which is used to provide the value.

Examples of DataPoints would be OrderNumber, OrderStatus, OrderExchange, etc.


DataPointSource
===============

A ``DataPointSource`` is a client-side code that provides a value for a named ``DataPoint``. It is an abstract class with a ``GetValue`` method that must be overridden. It also provides a ``SetStale`` method that is used to indicate to the ``ExecutionAgent`` that the value must be re-examined. This will cause any ``WorkingRules`` for Rule that has a dependency on this ``DataPoint`` to be the queue for re-evaluation on the next cycle.

The ``DataPointSources`` for the above example ``DataPoints`` would access the ``EMSX`` data to return the correct ``EMSX_SEQUENCE`` and ``EMSX_STATUS``, and perhaps use the reference data service to get the exchange code for the ticker on the order.


The ExecutionAgent process
==========================

When the application has completed the configuration of all the main elements (``Rules``, ``RuleConditions``, ``Evaluators``, ``Action``, 
``Executors``, and etc.), one or more ``RuleSets`` can be executed.

This involves taking a ``DataSet`` and asking the ``RuleSet`` to be executed against that DataSet: -

.. code-block:: none

	myRuleSet.Execute(dataSet_1);

If this is the first time this ``RuleSet`` has been executed, a new ``ExecutionAgent`` will be created for the ``RuleSet``. If the ``RuleSet`` already has an ``ExecutionAgent``, it will be reused. The specified ``DataSet`` is then passed to the ``RuleSet``'s ``ExecutionAgent``: -

.. code-block:: none

	executionAgent = new ExecutionAgent(myRuleSet, dataSet_1);


or

.. code-block:: none

	executionAgent.AddDataSet(dataSet_1);


Each ``ExecutionAgent`` has a ``DataSetQueue``. Adding a ``DataSet`` to an ``ExecutionAgent`` simply adds the ``DataSet`` reference into the ``DataSetQueue``. This is used to ensure that new ``DataSets`` are only ingested at the correct time, and not at the mid-point of a cycle.

A new ``ExecutionAgent`` will create a new internal thread that will operate a ``WorkingSetAgent``. This ``WorkingSetAgent`` is the main loop that controls the execution of the rules and actions for a ``RuleSet``, and it continues to run until stopped by an external request (a call to the ``stop()`` method).

Each cycle of the ``WorkingSetAgent`` begins with ingesting any ``DataSets`` in the ``ExecutionAgent``'s ``DataSetQueue``. This is the process of creating a ``WorkingRule`` for each Rule in the ``RuleSet`` and the specified ``DataSet``.

To create a ``WorkingRule``, a Rule and a ``DataSet`` are required. A process known as dereferencing takes place, which has two steps. The first step is to take each Action associated with the Rule and add the ``ActionExecutor`` references to the ``WorkingRule``’s Executors collection.

The second part of the dereferencing process is to iterate each ``RuleCondition`` of the Rule, and add it’s ``RuleEvaluator`` to the ``Evaluators`` collection of the ``WorkingRule``. Each ``RuleEvaluator`` has a collection of ``DataPoint`` names that it depends on. For each of these dependant data point names, we find the actual ``DataPoint`` in the ``DataSet`` that matches the name. The ``WorkingRule`` is then added to the ``AssociatedWorkingRules`` collection of the ``DataPoint``’s ``DataPointSource`` object.

The reason for doing this is that when a ``DataPointSource``’s value changes, its ``SetStale()`` method is (should be) fired. This forces each ``WorkingRule`` dependency of the ``DataPointSource`` to be added to the ``OpenSetQueue`` in the ``WorkingSetAgent`` for execution in the next cycle, unless the ``WorkingRule`` is already in the ``OpenSetQueue``.

Following the ingestion process, the current ``OpenSetQueue`` becomes the ``OpenSet``, and the``OpenSetQueue`` is then reset to empty. The ``OpenSet`` is now iterated, and each ``WorkingRule`` in the queue is processed. Each ``Evaluator`` in the ``WorkingRule`` is fired, passing it the ``WorkingRule``’s ``DataSet``. If all ``Evaluators`` in the ``WorkingRule`` return true, then the action process begins. Each action associated with the ``WorkingRule`` is executed.


RETE Algorithm
==============

The word rete is Latin for net or network. 
The rete algorithm is essentially a pattern matching algorithm. 

The main objective behind rete algorithm for RuleMSX is to decouple the various trading or business rules from rule execution or executing sequences on a particular data set. 

The data set here can be both trading data obtained from EMSX API, market data, or non-trading based proprietary data set.

The RuleMSX views each rule exists as a stand-alone rule that is either true or false at any given moment. 

A pattern contains one or more rules. All the rules in a pattern must evaluate to true for the action attached to the pattern to be executed. In this case, the action itself is responsible for introducing the new rules to be checked and/or new patterns or patterns to be removed from the set. 


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



