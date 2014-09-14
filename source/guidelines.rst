Guidelines
==========

Common JavaScript Trigger
-------------------------

Trigger are used to broadcast certain events

ajax.ready
	  Is triggered on the container, which is altered by the ajax.request.
          Remember, this event bubbles, so all listener on elements above will spring into action, too.




Naming Conventions
------------------


* Variables: lowerCaseStartingCamelCase like ....
* Modules and Classes: UpperCaseStartingCamelCase like FormularValidation
* Array keys (options arrays): underscore_separated ( 'option_key' )
* Service names Module/[SubCategory/]Service ok.
* Configuration Keys invocable form element: UpperCaseStartingCamelCase, <Module>/<Element> like 'Applications/Mail'
* Configuration Keys invocable controllers: UpperCaseStartingCamelCase, <Module>/<Element> like 'Applications/Mail'
* Configuration Keys view scripts: lowercase, dash-separated, like 'applications/index/disclaimer'



