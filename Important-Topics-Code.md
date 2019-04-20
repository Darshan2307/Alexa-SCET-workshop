**Fallback Intent** :  https://developer.amazon.com/docs/custom-skills/standard-built-in-intents.html#fallback

    
    const FallbackIntentHandler={
        canHandle(handlerInput){

            return handlerInput.requestEnvelope.request.type==='IntentRequest'&&
                   handlerInput.requestEnvelope.request.intent.name==='AMAZON.FallbackIntent';
        },
        handle(handlerInput){

            const say="Sorry I can't help you with that."
            return handlerInput.responseBuilder.speak(say).getResponse();

        }
    };
    
**Reprompt** : https://developer.amazon.com/docs/custom-skills/handle-requests-sent-by-alexa.html#listen-and-reprompt


    return handlerInput.responseBuilder
                .speak(say)
                .withSimpleCard("Facts",say)
                .reprompt("Would you like more facts?") //asks a question to the user for more facts.. Handle the response                                                              with other intent
                .getResponse();

**Including Cards in your response** : https://developer.amazon.com/docs/custom-skills/include-a-card-in-your-skills-response.html

**Setting card responses in code** : https://developer.amazon.com/docs/custom-skills/handle-requests-sent-by-alexa.html#speech-and-cards

   **Basic Card (without Image)**

    const say="Your content here";
        return handlerInput.responseBuilder
            .speak(say)
            .withSimpleCard("Card-title",say)
            .reprompt("Would you like more facts?")
            .getResponse();
    
    
   **Standard Card with Image**
      
      const say="Your card content here..";
       
       return handlerInput.responseBuilder
            .speak(say).withShouldEndSession(false).withStandardCard("Guess",say,
            "https://s3.amazonaws.com/asi-workshop/game.jpg")
            .getResponse();

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

