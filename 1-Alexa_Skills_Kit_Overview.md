# AlexaSkills
Researching and experimenting Alexa Skills, possible integrations with SDK from JS side or from python side



<h1> <a href= "https://www.youtube.com/watch?v=CzTKDu7Qgjs"> Zero to Hero, Part 1: Alexa Skills Kit Overview </a> </h1>

>   Skills are capabilities that developers give alexa

A skill is opened using the wake word to activate the device ("Alexa") + Invocation Name, a name the developer decides to give to the skill that needs to be said in order to open that specific skill (can be multiple words and can be generic, also invocation names do not have to be unique -> if multiple skills share the same invocation name, its up to the user to chose which skill they want to be activated)

>    Accessing a functionality within the skill is accomplished with a "one shot utterance"  (opening the skill and giving a command at the same time)

### Utterences map to "Intents" => There are various ways of saying the same thing, but all of them mean the same intent

>   ### As a developer, you need to decide what intent your skill supports (giving a fact, planning a trip, quitting, starting a new game, ...)


>   ### Example sentences are then given, that symbolize this intent


>   ### It is up to Alexa to route the user into the right intent


e.g. GetNewFactIntent

<hr />

#   That would be enough without satisfying certain information, hence "slots", which is the Alexa voice equivalent of a variable


>   ##  A variable is a piece of the user's utterence that we need as developers to fulfil that specific intent



>   ### We can have more than one slot in an intent, and users can specify more than one slots in their sentences (utterences)



<hr />

#   Recap with example:

1)  Alexa,      --> Wake word


2)  ask     --> launch


3)  space fact      --> invocation name


4)  for a fact about |_ _{planet} _|   --> utterance



>   #   As many intents as necessary can be added, but there are some already built in ones, some of which is mandatory to pass the certification process for the Alexa skill (help -> AMAZON.HelpIntent, cancel-> AMAZON.CancelIntent, stop -> AMAZON.StopIntent, ...), but there are also built in intents like "repeat" -> AMAZON.RepeatIntent, "shuffle", "get address",... 


>   ### Pre-built intents help us as developers not have to input every possible sentences for common utterances (like yes, no, repeat, shuffle, play, ...) as they are pretrained on a lot of utterances


<hr />


#   Building for Alexa has 2 sides:

##  1)  Voice Interaction Model: where we find skill name, invocation name, intents, slots, utterances,... everything related to the voice interface


##  2)  The Backend is where we implement and handle all these intents -->  Using @ <a href="developer.amazon.com">Alexa hosted skills</a> on Amazon! Meaning everything is hosted and managed for us


<hr />


#   File Structure of a Skill:

##   /models Folder:
                <!-- In here we have all of our interaction models, all the intents/utterances represented in a JSON file for each language that we choose to support -->

            /en.US.json


##  /lambda/custom
                <!-- The backend code is stored here in the lambda folder -->
            /index.js


##  skill.json


<hr />


