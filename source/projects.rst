########
Projects
########
There are currently three active projects written in C Sharp and Python. Other programming languages and projects will follow shortly.


Prerequisites
=============
* All C# projects requires .NET 4.0 but has no other external dependencies. 
* The python projects runs in Python 3. 


EasyMSX
=======
The EasyMSX allows getting orders, routes, and static data from EMSX API service. The EasyMSX allows adding notification handler on the real-time events. There is an `observer pattern`_ that can throw exceptions. 

.. _observer pattern: https://en.wikipedia.org/wiki/Observer_pattern


Installing
----------
* For C#, Download the source code and build the library from the source. Once the Bloomberg API SDK has been `referenced`_ in your project, create an instance of EasyMSX:-

* For python, create the new directory and extract easymsx-1.0.x into the new directory. Change the directory to easymsx-1.0.x and in the directory run the following command:-

.. code-block:: none

	C:\Users\Me\>cd easymsx-1.0.x

	C:\Users\Me\easymsx-1.0.x>C:\Python34\python.exe setup.py install

* Run easymsxdemo.py

.. code-block:: none

	C:\Users\Me\>cd easymeasymsx-1.0.x

	C:\Users\Me\easymsx-1.0.x>py -3 easymsxdemo.py

* The GitHub link to the EasyMSX sample in `EasyMSX`_.

.. _referenced: https://easymsx.readthedocs.io/en/latest/resources.html#net-reference-for-rulemsx-project
.. _EasyMSX: https://github.com/tkim/EasyMSXRepository


EasyMKT
=======
The EasyMKT and EasyMKTSample are essentially an EasyMSX for market data where the project demonstrates one possible way to build caching data on Bloomberg real-time market data.


Installing
----------
* For C#, Download the source code and build the library from the source. Once the Bloomberg API SDK has been `referenced`_ in your project, create an instance of EasyMKT:-

* For python, create the new directory and extract easymkt-1.0.x into the new directory. Change the directory to easymkt-1.0.x and in the directory run the following command:-

.. code-block:: none

	C:\Users\Me\>cd easymkt-1.0.x

	C:\Users\Me\easymkt-1.0.x>C:\Python34\python.exe setup.py install


* Run easymktdemo.py

.. code-block:: none

	C:\Users\Me\>cd easymsx-1.0.x

	C:\Users\Me\easymkt-1.0.x>py -3 easymktdemo.py

* The GitHub link to the EasyMKT sample in `EasyMSX`_.

.. _referenced: https://easymsx.readthedocs.io/en/latest/resources.html#net-reference-for-rulemsx-project
.. _EasyMSX: https://github.com/tkim/EasyMSXRepository


RuleMSX
=======
Rather than making use of domain specific language (DSL) to define the rules, it exposes a series of abstract classes. It facilitates the creation of complex if-this-then-that behavior.


Installing
----------
* For C#, Download the source code and build the library from the source. 

* For python, create the new directory and extract easymsx-1.0.0 and rulemsx-1.0.0 into the new directory.

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


* Change the directory to rulemsx-1.0.0 and in the directory run the following command:-

.. code-block:: none

	C:\Users\Me\_rulemsx>cd rulemsx-1.0.0

	C:\Users\Me\_rulemsx\rulemsx-1.0.0>C:\Python34\python.exe setup.py install

* Please make sure the path for python is set to where you currently have your python 3 installed. Change directory to easymsx-1.0.0 and in the diretory run the following command:-

.. code-block:: none
	
	C:\Users\Me\_rulemsx>cd easymsx-1.0.0

	C:\Users\Me\_rulemsx\easymsx-1.0.0>C:\Python34\python.exe setup.py install

* Run RuleMSXDemo.py

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


Getting Started
---------------
The following is the C# implementation of the RuleMSX sample. RuleMSX provides the core functionality of a rule engine. Once the library has been `referenced`_ in your project, create an instance of RuleMSX:-

.. _referenced: https://easymsx.readthedocs.io/en/latest/resources.html#net-reference-for-rulemsx-project

.. code-block:: c#

    RuleMSX rmsx = new RuleMSX();


RuleMSX is divided into 'Rules'_, 'DataPoints'_ and 'Actions'_. Rules are organized into 'RuleSets'_:-

.. _Rules: https://easymsx.readthedocs.io/en/latest/resources.html#rules
.. _Actions: https://easymsx.readthedocs.io/en/latest/resources.html#rules
.. _RuleSets: https://easymsx.readthedocs.io/en/latest/resources.html#rulesets


.. code-block:: c#

    RuleSet myRuleSet = this.rmsx.CreateRuleSet("MyRuleSet");

A RuleSet contains one or more Rules, and each Rule is made up of one or more `RuleConditions`_. Each RuleCondition has a `RuleEvaluator`_ which is the code written by the developer. Each rule also has one or more `RuleAction`_ associated with it. When all the RuleConditions are met, the RuleAction is excuted.

.. _RuleConditions: https://easymsx.readthedocs.io/en/latest/resources.html#ruleconditions
.. _RuleEvaluator: https://easymsx.readthedocs.io/en/latest/resources.html#ruleevaluator
.. _RuleAction: https://easymsx.readthedocs.io/en/latest/resources.html#ruleactions


To create a Rule:-

.. code-block:: c#

    Rule myNewRule = myRuleSet.AddRule("NewRule");



To create a RuleCondition:-

.. code-block:: c#

    RuleCondition myRuleCondition = new RuleCondition("MyConditoin", new MyCondtionCode());

The 'MyConditionCode' class extends the RuleEvaluator abstract class, guarenteeing the presence of an Evalute() method. This method must return a `boolean value`_.

.. _boolean value: https://en.wikipedia.org/wiki/Boolean_data_type

For example:-

.. code-block:: c#

    class MyConditionCode : RuleEvaluator
    {
        public MyConditionCode()
        {
            // constructor code
        }

        public override bool Evalute(DataSet dataSet)
        {
            if(<sometest>) {
                return True;
            }
            else 
            {
                return False;
            }
        }
    }


Add the RuleCondition to the Rule:-

.. code-block:: c#

    myNewRule.AddRuleCondtion(myRuleCondition);


Alternatively:-

.. code-block:: c#

    myRuleCondition.AddRuleConditino(new RuleCondition("MyCondition", new MyConditionCode()));


When the RuleEvaluator of each of the RuleConditions Associated with a Rule return True, then any Actions associated with the Rule will be fired.

Actions are created independently of a Rule, so that a single action can be reused across multipel Rules, An action consists of a Rule object, and an associated RuleEvaluator which is extended by the developer.

To create an Action:-

.. code-block:: c#

    Action myAction = rmsx.CreateAction("MyAction", new MyActionCode());

The 'MyActionCode' class extends the ActionExecutor abstract class, guarenteeing the presence of an Execute() method.

For example:-

.. code-block:: c#

    class MyActionCode: ActionExecutor
    {

        public MyActionCode()
        {
            // constructor code
        }

        public void Execute(DataSet, dataset)
        {
            // do something here
        }
    }


Add the Action to the Rule:-

.. code-block:: c#

    myNewRule.AddAction(myAction);

Alternatively:-

.. code-block:: c#

    myNewRule.AddAction(rmsx.CreateAction("MyAction", new MyActionCode()));

The data to be processed is a RuleSet is defined as 'DataPoints'_, which are organized into 'DataSets'_.

A DataPoint is a single named item of data that has an assocated DataPointSource. The DataPointSource is an abstract class that the developer extends, which guarentees teh presense of a GetValue() method. Think of the DataSet as an object with properties. Think of the DataSet as a collection of DataPoints, each of which is a key-value pair. 

.. _DataPoints: https://easymsx.readthedocs.io/en/latest/resources.html#datapoints
.. _DataSets: https://easymsx.readthedocs.io/en/latest/resources.html#datasets


You submit a DataSet for execution by a RuleSet's execution agent, as follows:-

.. code-block:: c#

    myRuleSet.execute(myDataSet);

To create a DataSet:-

.. code-block:: c#

    DataSet myDataSet = rmsx.CreateDataSet("<some unique name>");


To create a DataPoint, you first need to create a `DataPointSource`_. This is done by creating a class that extends DataPointSource:-

.. _DataPointSource: https://easymsx.readthedocs.io/en/latest/resources.html#datapointsource

.. code-block:: c#

    private class ConstantDataPointSource : DataPointSource
    {
        string retValue;

        public TestDataPointSource(string retValule)
        {
            this.retValue = retValue;
        }
        public override object GetValue()
        {
            return retValue;
        }
    }


An instance of thi sclass will return the value that was passesd to the constructor whenever the GetValue() method is called. 

Create the DataPoint as follows:-

.. code-block:: c#

    DataPoint myDataPoint = new ConstantDataPointSource("Return this!");

Add the DataPoint to the DataSet:-

.. code-block:: c#

    myDataSet.AddDataPoint("DataPoint1", myDataPoint);

Alternatively:-

.. code-block:: c#

    myDataSet.AddDataPoint("DataPoint1", new ConstantDataPointSource("Return this!"));


Operation
---------
The `execution agent`_ that underlies a RuleSet operates in its own thread. When a RuleSets Execute() method is first invoked, the execution agent is created. Thereafter, any further calls to Execute() will result in the DataSet simply being passed to the already running agent.

When a DataSet is ingested by the execution agent, all the Rules will be tested. Once a rule is tested, it will not be tested again, unless it is re-introduced. This happesn when a RuleCondition whin the rule has a delcared dependency on a DataPoint whos DataPointSource has been marked as stale. This is done on the client side, by calling SetStale() on a DataPointSource object. Any Rule that has a dependency on that DataPoint will be re-introduced into the queue of Rules to be tested.

This means that RuleCondition can be created that depends on  the value of a variable or field that will change over time. When the rule is fist tested, perhpas the value is in a state that means that the Evaluate() method will return False. However, it may change later. The rule will not be tested again under normal circumstances. But if the variable or field changes values, simply call the SetStale() method on the DataPointSource object, and any and all Rules which have a RuleCondition that depends on its value will be re-tested. This means that the RuleCondition may now return True, and the associated ActionExecutor of Rule will be fired. 

.. _execution agent: https://easymsx.readthedocs.io/en/latest/resources.html#the-executionagent-process

Tests 
-----
NUnit unit tests, as well as integration tests, are included in the project.

Deployment
----------
Simply distribute the library with any application distribution.

License
-------
This project is under the MIT License - see the License file for details.

