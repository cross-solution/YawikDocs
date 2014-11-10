Guidelines
==========

Programming Guidelines related to code-maintenance
--------------------------------------------------

* the content of the output is completely determined by the Controllers
    * Viewscripts do provide output, but they can be replaced by other viewscripts in the Controller, so the Controller is still in charge
    * a majority of viewhelper also do provide an output, but viewhelpers are still only active on demand.
    * a **nogo** are ubiquitous listener which are defined somewhere in the bootstrap-process and alter or extend the content, there is no point in trying to make them smart, this is just another cause for irratic behaviour
    * it is ok to offer some defaults for output, as long as these defaults can be altered in the Controller
* avoid distributed addressing by name-strings, it is just awkward to search for errors related to run-time definitions hidden all over the code
    * keep the defining of the behaviour for an entity in a small scope and use abstract handling of the behaviour anywhere else
    * throw exceptions if elements are addressed, which don't exist. Don't rely on purpose if something is missing - if something is optional, flag it as optional
* apply the rule of three
* prefer interfaces to constants for distinguishing code behaviour - interfaces may give you a runtime error if you have done something wrong
* allways use getter und setter, it is not just a principle of object-orientation (hiding), it is also easier to track down a call when debugging
* don't use exceptions as a regular programming flow, exceptions are exceptions - that implies something went wrong in the code, not by the use of the code


Common JavaScript Trigger
-------------------------

Trigger are used to broadcast certain events

ajax.ready
	  Is triggered on the container, which is altered by the ajax.request.
          Remember, this event bubbles, so all listener on elements above will spring into action, too.




Naming Conventions
------------------


* Variables: lowerCaseStartingCamelCase like ....
* Modules and Classes: UpperCaseStartingCamelCase
* Array keys (options arrays): underscore_separated ( 'option_key' )
* Service names Module/[SubCategory/]Service ok.
* Configuration Keys invocable form element: UpperCaseStartingCamelCase, <Module>/<Element> like 'Applications/Mail'
* Configuration Keys invocable controllers: UpperCaseStartingCamelCase, <Module>/<Element> like 'Applications/Mail'
* Configuration Keys view scripts: lowercase, dash-separated, like 'applications/index/disclaimer'



