# Impress AI Bot Assignment
This is the technical assignment for Impress AI

# Requirements

- Python 3
- Make sure you have pip (pip --version)
- pip install virtualenv to install virtual environment
- Telegram messenger (you can also use the web version at web.telegram.org)

## What to do

To get this running, you need the following. First install dependencies

### Step 0 : Clone the Repository

- `git clone https://github.com/markeyys/impressai-assignment.git`
- `cd impressai-assignment`

### Step 1 : Install dependencies

`pip install -r requirements.txt`

### Step 2 : Run migrations (optional actually)

Though there are no models for this code, this just creates the default stuff for admin.

`python manage.py migrate`

### Step 3 : Download and use ngrok

You need an HTTPS url for most webhooks for bots to work. For purely development purposes you can use ngrok. It gives a web-accessible HTTPS url that tunnels through to your localhost.
Download ngrok (https://ngrok.com/)  , got to a new tab on your terminal and start it with

`ngrok http 8000`

At this point, you will have to add the URLs to ALLOWED_HOSTS in `chatbot_tutorial/settings.py`.

### Step 4 : Start the local server

And start the server with

`python manage.py runserver`

### Step 5 : Talk to the BotFather and get and set your bot token

Start telegram, and search for the Botfather. Talk to the Botfather on Telegram and give the command `/newbot` to create a bot and follow the instructions to get a token.

Copy the token and paste in `chatbot_tutorial/views.py`

### Step 6 : Set your webhook by sending a post request to the Telegram API

Retrieve in the token and add it into `TELEGRAM_TOKEN` under `chatbot_tutorial/views.py`

If you are on a system where you can run a curl command, run the following command in your terminal (Remember to replace ngrok_url and bot_token)

`curl -F “url=<ngrok_url>/c817304a3d163ebd58b44dd446eba29572300724098cdbca1a/“ https://api.telegram.org/bot<bot_token>/setWebhook`

Alternatively, you can use some service like Postman or hurl.it just remember to do the following:

- Request type is "POST"
- url to post to https://api.telegram.org/bot<bot_token>/setWebhook
- as parameters add this (name, value) pair: (url, <ngrok_url>/c817304a3d163ebd58b44dd446eba29572300724098cdbca1a/)

You should get a response that states that "webhook has been set"

### Step 7 : Talk to the bot

You should now be able to talk to the bot and get responses from it

### Step 8: To View the users interacting with the bot and their total number of calls made
- Visit `localhost:8000/telegrambot`