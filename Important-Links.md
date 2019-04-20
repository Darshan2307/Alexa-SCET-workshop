**Fallback Intent** :  https://developer.amazon.com/docs/custom-skills/standard-built-in-intents.html#fallback

**Reprompt** : https://developer.amazon.com/docs/custom-skills/handle-requests-sent-by-alexa.html#listen-and-reprompt

**Including Cards in your response** : https://developer.amazon.com/docs/custom-skills/include-a-card-in-your-skills-response.html

**Setting card responses in code** : https://developer.amazon.com/docs/custom-skills/handle-requests-sent-by-alexa.html#speech-and-cards

**Using Session Attributes**: https://developer.amazon.com/blogs/alexa/post/08edaa00-59e2-46b7-aace-4080f2a87450/using-session-attributes-in-your-alexa-skill-to-enhance-the-voice-experience

**Code for Session Attributes**:

    const FavTeamIntentHandler={

      canHandle(handlerInput){

          return handlerInput.requestEnvelope.request.type==='IntentRequest'
                    && handlerInput.requestEnvelope.request.intent.name==='FavTeamIntent';
      },

      handle(handlerInput){
        
        //gets the session Attributes here which will be null at first.
        var attr= handlerInput.attributesManager.getSessionAttributes();
        
        //get the slot value of team slot

        const myTeam=handlerInput.requestEnvelope.request.intent.slots.team.value;
        
        //assign value of slot to session attribute "favTeam"

        attr.favTeam=myTeam;
        
        //set the session Attributes..

        handlerInput.attributesManager.setSessionAttributes(attr);

        return handlerInput.responseBuilder.speak("Thanks.")
              .withShouldEndSession(false)
              .getResponse();
      
      
  }
};

