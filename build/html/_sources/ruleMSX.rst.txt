#######
RuleMSX 
#######

RuleMSX views each rule exists as a stand-alone rule that is either true or false at any given moment. 

A pattern contains one or more rules. All the rules in a pattern must evaluate to true for the action attached to the pattern to be executed. In this case, the action itself is responsible for introducing the new rules to be checked and/or new patterns or patterns to be removed from the set. 

RETE Algorithm
==============

(More on RETE Algorithm)


Earlier Version
===============

The initial approach to RuleMSX handled the rete in the following structure


.. image:: /image/RuleMSX.png


As part of the reiteration of RuleMSX, we have made the changes to reflect the rete algorithm in the following structure: 


.. image:: /image/RuleMSXNew.png



 


