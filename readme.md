## Event Listener Process Template
This project includes a very basic Red Hat Process Automation Process template for Event Listeners demonstration.

Process has 4 assets:

 1. The business process file
 2. Drools file
 3. A data object as "Message"
 4. An auto created work item definitions file

![assets](https://raw.githubusercontent.com/mabulgu/eventlistenerprocess/master/images/assets.png)

In this template we have 4 listeners for demonstration. 3 of them are event listeners and one of them is an implementation of task listener:

 1. CustomProcessEventListener
 2. CustomAgendaEventListener
 3. CustomRuleRuntimeEventListener
 4. CustomTaskLifeCycleEventListener

![listeners](https://raw.githubusercontent.com/mabulgu/eventlistenerprocess/master/images/listeners.png)

![task_listener](https://raw.githubusercontent.com/mabulgu/eventlistenerprocess/master/images/task_listener.png)


As for the business process has the following structure:

![process](https://raw.githubusercontent.com/mabulgu/eventlistenerprocess/master/images/process.png)

There is a process variable called "message" with a type of Message object. At the start of the process either we initiate it or not with the following script task we set the text variable like the following:

![script_task_details](https://raw.githubusercontent.com/mabulgu/eventlistenerprocess/master/images/script_task_details.png)

By setting this variable's text field, we assure the next rule task to match the rule succesfully so that we can see the CustomAgendaEventListener and the CustomRuleRuntimeEventListener events are triggered.

![rule](https://raw.githubusercontent.com/mabulgu/eventlistenerprocess/master/images/rule.png)

After the business rule task, the process stops and waits for a human task that will help us with triggering some CustomTaskLifeCycleEventListener events like releasing the task or claiming it.

![process_human_task](https://raw.githubusercontent.com/mabulgu/eventlistenerprocess/master/images/process_human_task.png)

After starting the process and doing some claim, release, suspend actions on the relevant task the total custom listener output is like this:

![console_output](https://raw.githubusercontent.com/mabulgu/eventlistenerprocess/master/images/console_output.png)

All the custom event listeners do just implement the relevant interfaces and methods just print the relevant topic's (process, task, rule, variable etc.) status for the demonstration. 

The event listeners are packed as a seperate template project within this repository: 
[https://github.com/mabulgu/customeventlisteners](https://github.com/mabulgu/customeventlisteners)

So before running the EventListenerprocess since a dependency is added for CustomEventListeners project, it has to be imported in the artifact repository that Process Automation Manager installation uses. The following image demonstrates the M2 Repository content of PAM that has the CustomEventListeners dependencies.

![pam_repo](https://raw.githubusercontent.com/mabulgu/eventlistenerprocess/master/images/pam_repo.png)

