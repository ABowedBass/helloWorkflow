# Best Practices

## Descriptions/Readme:
  * Make sure descriptions and readme are, you guessed it, descriptive.
      * Give an overview of the whole workflow process, which may entail multiple workflows
      * **IMPORTANT** Import order is very important for workflows. If a workflow calls a subflow, that subflow _must_ be in Reach Engine before importing the parent. It will fail to import otherwise
      * Descriptions:
          * User Inputs to the workflows
          * Are there any necessary system configurations that need to be added for the workflow to function?
          * Describe the workflows (typically starting with the parent and going down the chain to all of the workflows involved in the process)
      * The Flow of work, from once workflow to the next.

* Comments:
  * Just like any other traditional programming language, comments help anyone else who is looking at your code
  * \<!-- we are looking at this comment that is showing how to comment out a comment with the hopes that this comment accurately depicts a comment -->
  * very helpful when looping within the workflow \<!-- here is the start of a loop and it's conditions for when it will loop or exit --> _THELOOP_THATISLOOPING_ \<!-- here is the end of the loop and the conditions to loop or to exit -->

* Step Names:
    * Make Step names descriptive:
        * If a convertVideoStep is transcoding a proxy video file, name the step accordingly:
            * name="create proxy" or "generate proxy"

* Transitions:  
    * Transitioning using a noopStep vs transitions within a step:
        * A noopStep is its own step that moves the workflow to different steps based on a logical evaluation:
            * Example of a transition using a noopStep, see example 1 in workflowExamples
        * Transitioning within a step is _essentially_ like having a noopStep within the step that you are using
            * Example of a transition within a step, see example 2 in workflowExamples
    

* Versioning (GitHub)
    * Any questions?
      * Fork --> clone --> branch --> add --> commit --> push to branch --> PR

* Logging
    * Test steps
    * Execution Labels
    * println
    * log4j

* End
