===============================================================================
Persistent Identification of Instruments (PIDINST) Cookbook
===============================================================================

.. sectnum::

+------------------+-------------------------------------------------------------------------------+
|Document type     |Research Data Alliance (RDA) Persistent Identification of Instruments (PIDINST)|
|                  |working group output report                                                    |
+------------------+-------------------------------------------------------------------------------+
|Version           |2.0                                                                            |
+------------------+-------------------------------------------------------------------------------+
|Date              |19 February 2020                                                               |
+------------------+-------------------------------------------------------------------------------+

Introduction
~~~~~~~~~~~~
This cookbook enables instrument providers to create persistent identifiers (PID) for instruments using the ePIC infrastructure [1]_. ePIC is an international consortium that provides PID services for the worldwide research community, allowing them to allocate and resolve PIDs based on the handle system (TM, https://www.handle.net/). In 2019, ePIC published a metadata schema for citing instruments, as part of the recommendations resulting from the Research Data Alliance working group for the persistent identification of instruments (PIDINST) [2]_ referred to as the PIDINST metadata schema [3]_. This document provides technical guidance for publishing instrument PIDs through ePIC.


PIDINST handles at ePIC
~~~~~~~~~~~~~~~~~~~~~~~
Properties, sub-properties and attributes of the PIDINST metadata schema used in ePIC PID handle records can be viewed as follows. Use ‘#’ before ‘objects’ to interchange between human-readable and JSON representations. Each property, sub-property and attribute is resolvable through a unique handle record:

+----------------------+---------------------------------------------------------------------------+
|Human-readable        |http://dtr-test.pidconsortium.eu/#objects/21.T11148/17ce618137e697852ea6   |
+----------------------+---------------------------------------------------------------------------+
|JSON representation   |http://dtr-test.pidconsortium.eu/objects/21.T11148/17ce618137e697852ea6    |
+----------------------+---------------------------------------------------------------------------+


Generating a new instrument PID
-------------------------------
ePIC handles are accessed and managed via a RESTful web service, using the HTTP application protocol. This service or Application Programming Interface (API) uses JSON as the primary exchange format. Available are the generic and more basic Handle API or, if implemented at the PID service used, the ePIC API that comes with its own business logic and additional services. In our following examples PIDINST handles are created via the ePIC API  in the ePIC API test environment with a view to moving the architecture to the production environment in the future. There is also an overview for the basic CRUD operations on PIDs for either the ePIC API or the Handle API at the end.

In order to generate new PIDs and assign them to your instruments, it is necessary to become an ePIC member (provider), or work with one of their current members or repositories that has their own ePIC API endpoint. To create a PID using the test environment you will need to obtain credentials (username and password) for authentication using the test environment prefix 21.T11998. These can be obtained from ePIC by emailing support@pidconsortium.net.

PIDs are typically created using POST/PUT methods. Using the POST method will automatically generate a Universally Unique Identifier (UUID) within the suffix of a handle record. Alternatively a suffix can be manually created via PUT method using a local identifier (see https://doc.pidconsortium.eu/guides/api-create/). 

All examples below use cURL requests at the command line (in Linux). Requests can also use PHP, Perl and Python (see https://doc.pidconsortium.eu/guides/api-create/). Examples also use the test API endpoint http://vm04.pid.gwdg.de:8081/handles/. Each ePIC member may use their own API end-point. 


To generate a PID handle record automatically generating a UUID for the suffix:
::
	curl -v -u "username:password" -H "Accept:application/json" -H "Content-Type:application/json" -X POST --data '[{"type":"URL","parsed_data":"https://linkedsystems.uk/system/instance/TOOL0022_2490/current/"}]' http://vm04.pid.gwdg.de:8081/handles/21.T11998/
*Note: Test API (http://vm04.pid.gwdg.de:8081/handles/)and test prefix (21.T11998) used.*
	
..	[1] https://www.pidconsortium.net/
..	[2] https://www.rd-alliance.org/groups/persistent-identification-instruments-wg
..	[3] https://github.com/rdawg-pidinst/schema

