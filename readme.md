## Event Listener Process Template
This project includes a very basic Red Hat Process Automation Process template for Event Listeners demonstration.

Process has 4 assets:

 1. The business process file
 2. Drools file
 3. A data object as "Message"
 4. An auto created work item definitions file

[assets image here]

In this template we have 4 listeners for demonstration. 3 of them are event listeners and one of them is an implementation of task listener:

 1. CustomProcessEventListener
 2. CustomAgendaEventListener
 3. CustomRuleRuntimeEventListener
 4. CustomTaskLifeCycleEventListener

[listener images here]

As for the business process has the following structure:

[business process image here]

There is a process variable called "message" with a type of Message object. At the start of the process either we initiate it or not with the following script task we set the text variable like the following:

[script task image details here]

By setting this variable's text field, we assure the next rule task to match the rule succesfully so that we can see the CustomAgendaEventListener and the CustomRuleRuntimeEventListener events are triggered.

After the business rule task, the process stops and waits for a human task that will help us with triggering some CustomTaskLifeCycleEventListener events like releasing the task or claiming it.

[task stopped image]

After starting the process and doing some claim, release, suspend actions on the relevant task the total custom listener output is like this:

[console output image]

All the custom event listeners do just implement the relevant interfaces and methods just print the relevant topic's (process, task, rule, variable etc.) status for the demonstration. 

The event listeners are packed as a seperate template project within this repository: [https://github.com/mabulgu/customeventlisteners](https://github.com/mabulgu/customeventlisteners)

So before running the EventListenerprocess since a dependency is added for CustomEventListeners project, it has to be imported in the artifact repository that Process Automation Manager installation uses. The following image demonstrates the M2 Repository content of PAM that has the CustomEventListeners dependencies.

[m2 repo image]

