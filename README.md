# Dialogflow reference connection code

You can use the Dialogflow reference connection code to connect a Vonage Voice API call to a Google Dialogflow agent and then have an audio conversation with the agent. Speech transcripts and sentiment analysis are posted back to the Vonage Voice API application.

## About this reference connection code

Dialogflow reference connection makes use of the [WebSockets feature](https://docs.nexmo.com/voice/voice-api/websockets) of Vonage Voice API. When a voice call is established, a Voice API application triggers a WebSocket connection to this Dialogflow reference connection and streams the audio to and from the voice call in real time.

See the [**sample Voice API application**](https://github.com/nexmo-community/dialogflow-sample-voice-application) for a  using this Dialogflow reference connection code to connect voice calls to a Google Dialogflow agent.

## Transcripts and sentiment scores

This reference connection code will send caller's speech transcript and sentiment score, and Dialogflow agent's transcript to the Voice API application via webhook calls.

## Dialogflow agent

You may already have a Google Dialogflow agent ready, if not, please create one that will be used for the purpose here.

For the next sections, we will need the corresponding Google Cloud Project ID value as well as Google Application Credentials JSON file (actual credentials file name has ".json" extension).

To retrieve them:</br>
- Go to the [dialogflow console](https://dialogflow.cloud.google.com), go to the relevant Dialogflow agent, click on the gear icon, you will see the Project ID, we will use that value to set the parameter **GCLOUD_PROJECT_ID** in the next sections,</br></br>
- To retrieve the application credentials:
click on the Project ID link (as mentioned above),</br>
click on '-> Go to project settings',</br>
'Service Accounts',</br>
'+ CREATE SERVICE ACCOUNT',</br>
enter a name for 'Service account name' , e.g. *VonageDF*</br> 
click CREATE</br>
select 'Dialogflow API' client as role (note: role permissions are beyond the scope of this demo)</br>
click CONTINUE</br>
click DONE</br>
click on the 3 vertical dots (under Actions), Create key, JSON, CREATE, save the created file in your application folder</br>
that key file name (ending with .json) is the value, e.g. *mydfagent-vonage-05768e59b7c5.json*</br>
we will use that value to set the parameter **GOOGLE_APPLICATION_CREDENTIALS** in the next sections.</br></br>

## Enabling APIs on your Google project

Using your Google Cloud Console, on your corresponding Google project, make sure that both the **Dialogflow API** and the **Cloud Natural Language API** are enabled.

## Running Dialogflow reference connection code

You deploy the Dialogflow reference connection code in one of the following couple of ways.

### Local deployment

To run your own instance of this sample application locally, you'll need an up-to-date version of Node.js (we tested with version 14.3.0).

Download this sample application code to a local folder, then go to that folder.

Copy the `.env.example` file over to a new file called `.env`:
```bash
cp .env.example .env
```

Edit `.env` file, and set both parameter values:</br>
GCLOUD_PROJECT_ID= </br>
GOOGLE_APPLICATION_CREDENTIALS=xxxxxxxxxxxxxxx.json</br>

Install dependencies once:
```bash
npm install
```

Launch the applicatiom:
```bash
node df-connecting-server
```

### Command Line Heroku deployment

You must first have deployed your application locally, as explained in previous section, and verified it is working.

Install [git](https://git-scm.com/downloads).

Install [Heroku command line](https://devcenter.heroku.com/categories/command-line) and login to your Heroku account.

If you do not yet have a local git repository, create one:</br>
```bash
git init
git add .
git commit -am "initial"
```

Start by creating this application on Heroku from the command line using the Heroku CLI:

```bash
heroku create thisappname
```

Note: In above command, replace "thisappname" with a unique name on the whole Heroku platform.

On your Heroku dashboard where your application page is shown, click on `Settings` button,
add the following `Config Vars` and set them with their respective values:</br>
GCLOUD_PROJECT_ID</br>
GOOGLE_APPLICATION_CREDENTIALS</br>

Deploy the application:

```bash
git push heroku master
```
