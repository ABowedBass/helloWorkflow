## Best Practices

* Descriptions/Readme:
  * Make sure descriptions and readme are, you guessed it, descriptive: Describe what the workflow is designed to accomplish, any necessary configurations, etc

* Comments:
  * Just like any other traditional programming language, comments help anyone else who is looking at your code
  * \<!-- we are looking at this comment that is showing how to comment out a comment with the hopes that this comment accurately depicts a comment -->
  * very helpful when looping within the workflow \<!-- here is the start of a loop and it's conditions for when it will loop or exit --> _THELOOP_THATISLOOPING_ \<!-- here is the end of the loop and the conditions to loop or to exit -->

* Step Names
  *  
    * If a convertVideoStep is transcoding a proxy, name the step accordingly:
        * name="create proxy" or "generate proxy"
    * A noopStep is transitioning based on whether a file exists within the managed repo or not:
        * name="check if file exists"
    * Transitioning using a noopStep vs transitions
    * Example of a transition using the noopStep above:
    \<!-- check if file exists
              if true, go to step name="continue processing"
                else, go to step name="error handling / fail step" -->
    <noopStep name="check if file exists"
      executionLabelExpression="Check if ${yourFile.absolutePath} exists"
      \>
      <transition condition="${yourFile.exists()}">\<!-- if true, go to continue processing -->
        <targetStepName>continue processing</targetStepName>
      </transition>
      <transition condition="${true}">\<!-- if the above condition is false, default to true here | ALWAYS HAVE THE LAST TRANSITION DEFAULT TRUE -->
        <targetStepName>error handling / fail step</targetStepName>
      </transition>
    </noopStep>
    \<!-- can have as many transitions as necessary -->

    Real world example:
    <setContextData name="determine media type"
	                targetDataDef="mediaType"
	                valueExpression="${#mediaType(fileToIngest)}"
		\>
		<transition condition="${mediaType == 'VIDEO'}">
			<targetStepName>ingest video asset</targetStepName>
		</transition>
		<transition condition="${mediaType == 'AUDIO'}">
			<targetStepName>ingest audio asset</targetStepName>
		</transition>
		<transition condition="${mediaType == 'IMAGE'}">
			<targetStepName>ingest image asset</targetStepName>
		</transition>
		<transition condition="${mediaType == 'DOCUMENT'}">
			<targetStepName>ingest document asset</targetStepName>
		</transition>
		<transition condition="${true}">
			<targetStepName>ingest other asset</targetStepName>
		</transition>

	</setContextData>

* Versioning (GitHub)
    * Any questions?
      * Fork --> clone --> branch --> add --> commit --> push to branch --> PR

* Logging
    * Test steps
    * Execution Labels
    * println
    * log4j

* End
