# Training Hello Workflow

## Workflow Overview
These workflows are designed to show different ways that variables can be set, passed down to subflows, and returned to the parent workflows. They also show how to use some of the different ways to print out values to different places (Reach Engine Logs, Catalina Logs, and execution label expressions). The end result will be transforming a string to equal 'Hello World'. If 'Hello World' is not the resulting string of the workflow, the workflow will fail.

## Import Order
1. helloWorldWorkflow
2. helloWorkflow


## Descriptions
#### User Input
* User adds a string to "Hello Workflow Input:" field on the user input form and selects either yes (true) or no (false) from "Allow Subflow Processing:". "Hello Workflow Input" has a default value built into the workflow, but will be overwritten by anything the user adds in. "Allow Subflow Processing" has a default value of true.

#### Result
* These workflows process the inputs given by the user input form to equal "Hello World", as long as allowSubflowProcessing == true

#### Sysconfig
* Here are the sysconfigs necessary:

workflow.defaultUserHello=Hello Workflow
workflow.groovyHello=Groovy Hello

#### helloWorkflow (parent workflow)
##### Initial step
* checks the value of userHello
    * If userHello == "Hello Workflow", go to 'set hellowWorkflow' step
    * Else, go to 'groovy hello' step

* 'set helloWorkflow'
    * sets 'helloWorkflow' variable to the value of 'userHello'
      * go to 'test hello'
* 'groovy hello'
    * sets 'helloWorkflow' variable to the value of 'groovyHello'
      * go to 'test hello'

* 'test hello' is hit by both of the above steps and prints out the value of 'userHello' and 'helloWorkflow' to the Reach Engine Logs
    * go to 'hello workflow to hello world'

* 'hello workflow to hello world' sends the value of 'helloWorkflow' and 'allowSubflowProcessing' to a subflow, "helloWorldWorkflow"
    * returns the outcome of the subflow to the data def 'helloWorld'
      * go to 'set success or failure'

* 'set success or failure' sets the value of a boolean-type variable, 'success', based on whether the value of 'helloWorld' is equal to 'Hello World'
    * If 'success' == true  
        * go to 'we won' and then end
    * Else, go to 'we lost' which is a failWorkflowStep


#### helloWorldWorkflow
* uses the value of 'helloWorkflow'(which will either be 'Groovy Hello' or 'Hello Workflow') to parse the string to the value of 'Hello World'


### Flow:
1) helloWorkflow -->
2) helloWorldWorkflow --> passes it's result back to helloWorkflow
