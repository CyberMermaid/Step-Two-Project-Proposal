# Step-Two-Project-Proposal
This is a proposal for my first Capstone project.

The goal of my website is to build a practical AI messaging application which integrates Twilio's SMS messaging service for communication with SpaCy library's natural language processing (NLP) techniques to create an intelligent chatbot that responds to its consumers in a user-friendly manner. and Flask for web application development. The chatbot UI is built with React while the backend REST API is built using Flask and Python to process and respond to messages.

Q: What kind of users will visit your site? In other words, what is the demographic of your users?
A: The demographic of users who will visit my site tend to be businesses and professionals in their late 20s to 40s. Businesses stand out as a target client as they need to be responsive to their consumers's needs. Also, professionals may need this application to keep their employers, coworkers, and clients satisfied especially if they travel a lot.

Q: What data do you plan on using? You may have not picked your actual API yet, which is fine, just outline what kind of data you would like it to contain.

Some data that I intend to use include text messages from users, named entities customized via the SpaCy library such as RECIPIENT_PHONE and MESSAGE, and specific words or phrases (strings like SEND TO +). 

4. (a) What does your database schema look like?

My database schema will most likely include the following tables Users, Messages, Intents, Entities, and Responses. 

 **Users**: Stores information about each user along with relevant user details.
 - id (Primary Key)
 - name
 - phone_number (Unique to avoid data redundancy and potential inconsistencies.)
 - created_at
 - updated_at

 **Messages** keeps track of all incoming and outgoing messages including responses generated by AI.
 - id (Primary Key)
 - user_id (Foreign Key referencing Users)
 - body
 - from 
 - to_recepient (Foreign key referencing phone_number in Users)
 - direction (incoming or outgoing)
 - created_at
 - updated_at

 **Intents**: Stores the intent from user's messages so that AI can process them. 
 - id (Primary Key)
 - name
 - user_name (Foreign key referencing Users)
 - created_at
 - updated_at

**Entities**: Logs the named entities extracted from the user's messages using Named Entity Recognition (NER). This table could store specific details extracted from the text, such as dates, locations, or names.
 - id (Primary Key)
 - message_id (Foreign Key referencing Messages)
 - type (e.g., date, location, person)
 - Recipient Phone (Foreign Key referencing Users)
 - value
 - created_at
 - updated_at

 **Responses**: Contains predefined responses that the AI can send back to the user based on the intents and entities identified in the user's messages.
 - id (Primary Key)
 - intent_id (Foreign Key referencing Intents)
 - content
 - created_at
 - updated_at

4. (b) What kinds of issues might you run into with your API?
   -**Lack of network readiness** My network needs to be ready to meet Twilio's Security and Webhooks security requirements including HTTPS/TLS, certificates, cipher suites, and request validation.
   -**Uncontrolled access to my Twilio account**. To get around this security issue, Twilio recommends using API keys, using Account SID and Auth Token to validate incoming requests to ensure they are genuine.
   -**Unnecessary Fetching**. To avoid unnecessary fetching that stems from making a large number of GET requests, Twilio recommends implementing webhooks or _StatusCallback requests_ for the resource endpoints that my account is using. This can reduces costs and improving efficiency. If I frequently fetch the same data from Twilio, Twilio recommends the business practice moving the data to my servers for enhancedd privacy, security, and compliance.
-**Exceeding Rate Limits**: Exceeding the rate limits of Twilio's products could lead to request failures. To prevent this from happening, I will have to look at the specific product API documentation to find the rate limits. Then, I will have to implement retries to ensure deliverability. 
-**Warnings or Errors**: A troubleshooting best practice is to implement the Account Debugger Webhook to send any warnings or errors directly to my servers. Twilio also provides SDK usage guides for instructions on debugging, exception handling, and returning header information in the SDK usage guides (found in the left-hand navigation bar under each SDK). This can be particularly useful for troubleshooting issues and escalating them to support if necessary 1.
4. (c) Is there any sensitive information you need to secure?
  **Yes**. Sensitive information that need to be secured are the API keys when using REST API for either a master or/and a subaccount, Webhook URLs, Encrypted Communication, and HTTP Authentication.
4. (d) What functionality will your app include?
   The AI messaging app developed using Spacy NLP, Twilio, and Flask will include functionality for:
   
- **Sending and Receiving Messages**: The app allows users to send messages to specific phone numbers using natural language commands. Spacy NLP is used to parse the user's input, extract the message content and the recipient's phone number. This functionality is demonstrated through examples where users can send messages like "Send a message to +15551234567 with the message 'Hello'".

- **User Interface**: The chat interface is built with React to providing a user-friendly way to interact with the app. After users send messages, the chat history display will includes both user inputs and bot responses. This interface includes elements for the chat container, header, body, and input section, with styling for user and bot messages.

- **Backend Functionality**: The backend server is set up with Flask which handles the logic for sending messages through Twilio's API based on the input received from the frontend. If there is a valid message and recipient phone number, Twilio's services will send the message.
  
- **Error Handling**: The application includes error handling for cases where the input is missing a message or the Twilio credentials are invalid. It provides feedback to the user in these scenarios to ensure a seamless user experience.

- **Training a Custom Named Entity Recognition Model**: The app uses Spacy NLP to train a custom model for named entity recognition to understand and extract information from user messages for sending SMS messages. This model is trained on a dataset of example sentences to recognize entities like phone numbers and messages within the text.

- **Future Enhancements**: The article suggests potential future enhancements for the app, including sentiment analysis, intent detection, language translation, and improvements to the user interface such as message threading, emojis, and user profiles. These enhancements aim to deepen the application's understanding of user messages and provide a more dynamic and engaging chat experience.

In summary, this AI messaging app incorporates Spacy NLP for entity recognition, Twilio for messaging capabilities, and Flask for backend development. This integration ensures a seamless and user-friendly experience for sending messages through natural language commands.

4. (e) What will the user flow look like?
   The user flow includes getting a free Twilio number, setting up the project by creating and training the AI Model with Spacy for natural language processing (NLP), building the backend REST API with Flask and Python, building the chatbot UI with React, and testing the AI pwoered messaging app.

4f. What features make your site more than CRUD? Do you have any stretch goals?
   My AI messaging app stands out beyond CRUD with its Spacy's NLP feature, Twilio's SMS Messaging service, Flask backend framework for a seamless integration of NLP combined with Twilio's messaging functionality, and the chatbot user interface that's been created with React.
   
   One stretch goal is definitely intent detection as I rarely see it mentioned in Twilio's blog (third link). Another stretch goal is to widen my application's functionality by integrating it with other messaging platforms like WhatsApp.
   
Sources: 
- https://www.twilio.com/docs/usage/rest-api-best-practices
- https://www.twilio.com/docs/usage/security
- https://www.twilio.com/en-us/blog/ai-messaging-app-sms-spacy-nlp-flask 
