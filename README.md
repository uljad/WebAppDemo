# Uljad Berdica
## ub352
# Flask-MongoDB Web App

## Disclaimer
The application should be live at the [CIMS server](https://i6.cims.nyu.edu/~ub352/WebAppDemo/flask.cgi), on https://i6.cims.nyu.edu/~ub352/WebAppDemo/flask.cgi. 

However, as I was testing the CRUD operations, the server stopped working and gave an *"internal Server Error message"*. I chose to create a separated repository for my App to make the CIMS connection much more efficiently. This Internal Error was unexpected. The App along with its webhook worked very well when tester by the tutor Vikas during office hours. 

I would kindly as you to not deduct points due to the unpredictable nature of this issues and inability to do anything about it. I worked on this assigment until 4am today (Dec 7th) and there was no possbility to contact anyone at 3 am (when the error first occurred.)

Forunately, just by making a .env file (copy of the env.example) with the following content, the app can be run locally with the `flask run` command and be live at  http://127.0.0.1:5000/ .

```
MONGO_HOST=class-mongodb.cims.nyu.edu:27017
MONGO_USER=ub352
MONGO_PASSWORD=qATAmUMI
MONGO_DBNAME=ub352
FLASK_APP=app.py # the main script file
FLASK_ENV=development # either development or production
GITHUB_SECRET=foo # pick any secret key word you like for GitHub webooks
GITHUB_REPO=https://github.com/uljadberdica1000/WebAppDemo.git # the GitHub repository
```

Thus, can use the local run to test the app, everything should work properly without the *server error* danger. 

## App Description 

This App is designed to work as a MongoDB based student message board. The main purpose of this application is to share information and preserve the anonimity of its users. Each document of the `posts` collection in the `ub352` database has the following atributes: "Type","username","date","content","urgency","tagged","password"

The main purpose of this app is to share information to a close community. The user can choose an anonymous identifier or put their own name.

### Password

The optional password is in case the user wants to keep the editing privileges to their message. The update process form requires dhe password for the `find_one_and_update` function to make an update. Otherwise, the upsert is set to true and a new post is added with the duplicate message. If the password is correct, the existing message is updated with the string  of `edited` concatenated next to the type/genre of the message i.e HW, Movies, Books etc. 

For example an updated post about Movies would say `Movie (Edited)`
This is a deliberate choice to preserve the transparency of information and its progress in time. If the user decides to not put a password when creating their message and putting it on the board for the first time, the message cannot be changed and can only be referenced or duplicated (or the user can tag himself in the tagg field of the document)

# CRUD

## Create

A form is displayed for the user to fill in the fields and then click submit

## Read

The 20 most recent messages are displayed. Every time an Update or Delete or Create form is filled out, the real time message board is showcased. 

## Update

A form is used as described in the Password section

## Delete

Since information is important, the only time a message can be deleted is if the used has the password, the content they wish to delete and the username of the document to be deleted. Only then is that document deleted. The `delete_one()` is used since I made the assumption that the same username would not post the same message on the board more than once since that would be spamming and be against the guidelines. If that assumption would not be valid, then the `delete_one` would be replaced by `delete_many`.

# Front_End

Due to the server Errors I could not implement the [JavaScript part](https://codepen.io/Zillionx/pen/xwOxoW) for the conditional forms. I created specific classes for each part of the app and then implemented the hover animations and tried to change the template as much as possible. 

I tried to make the webpage responsive to user interaction as advised by the tutors. 

## Mock Data

1000 Entries were generated using Mockaroo from this [schema](https://mockaroo.com/bb59b370)

create the `.env` and `run flask` to enjoy! The i6 hosted website was working until today at 4 am. I tried reverting to the point where it last worked and it still gives an error. 

Final Submission 10 am, Dec 7

