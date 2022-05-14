<h1> <a href= "https://www.youtube.com/watch?v=NXVmHWZZcjw"> Zero to Hero, Part 2: Skill Internationalization (i18n), Interceptors & Error Handling </a> </h1>




### Easier to do Internationalization in the beginning before adding new features


### In a simple hello world skill, we can see the summary of the interaction model in the JSON Editor


####    To add english USA for instance, since its also english and everything pretty much stays the same, we copy the UK language support interaction model from the JSON Editor  -->  Go to language settings  -->  Add new language (e.g. English USA)  -->  Go to English USA and paste the updated interaction model in the JSON Editor  -->  Save model and build!



>   ### For different languages that are not english based, we have to add different interaction models all together, but will follow the same process of adding a new language



<hr />

#   In each handler of the sample hello world, we have hardcoded strings -->  This will work fine for eng US and UK but not for other languages


##   How to internationalize the backend parametrizing specific strings and seperating them from the logic, especially in the case of adding a different language support for instance and need to introduce it?


>   ##   A dependency called "i18next", by adding either a node module dependency in the package.json or any corresponding dependencies file depending on language being used  --> Add dependency then deploy right away as adding a new dependency slows down deployment due to the amount of resources being used to add that dependency


>   ##  After adding the dependency of "i18next", we need to require it in the index.py/js file and create a language strings object in the case of adding new language support to the backend. It should include the language code for each language we are going to support


>   ##  We can also have more specific strings of different flavors of the same language (en US, en UK)  -->    We need string ids for that, which are present for instance in the translation object inside each locale, we need to choose which one we want to use in our code.  -->  Can be personalized




```


const i18n = require('i18next')

const languageStrings = {
    'en': {

    },
    'it': {

    }

}



```


<hr />


>   ##  From our handlers we just want to reference the string ids (WELCOME_MSG, HELLO_MSG, GOODBYE_MSG, ...)   --> For that we need to make sure that each handler knows that this language for instance already exists, and how to tie this language strings object to our i18next localization library?


#   This can be accomplished with an "Interceptor":

>   ##  An interceptor is a function that runs anytime either a request comes in (request interceptors  -->  before the handlers have handled anything) or a response goes out (response interceptors  -->  right after the handlers have handled what they need to handle, right before the actual skill response is sent to the Alexa service)


>   ##  Interceptors are great ways to have common code that can be used across handlers in one single point


####    In the e.g. of language support addition, we ll use a localization interceptor


>   ### The interceptor takes in a process() method --> meaning as the interceptor is run we have a handler input that we can manage however we want, and we also have to register it


<hr />

>   ##  This request interceptor will bind a translation function 't' to the handlerInput:

```



const LocalisationRequestInterceptor = {
    process(handlerInput) {
        i18n.init({
            lng: Alexa.getLocale(handlerInput.requestEnvelope),
            resources: languageStrings
        }).then((t) => {
            handlerInput.t = (...args) => t(...args);
        });
    }
};


exports.handler = Alexa.SkillBuilders.custom()
    .addRequestHandlers(
        LaunchRequestHandler,
        HelloWorldIntentHandler,
        HelpIntentHandler,
        CancelAndStopHandler,
        ...
    )
    .addRequestInterceptors(LocalisationRequestInterceptor)
    .addErrorHandlers(
        ErrorHandler,
    )



```







