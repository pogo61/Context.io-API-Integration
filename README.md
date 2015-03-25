# Akana API HOOK
![Image of Akana] 
(https://www.akana.com/img/formerlyLOGO8.png) 
[Akana.com](http://akana.com)

## Context.io API Integration
### About the API
- Build awesome things with email
- Home Page: [Context.io] (https://context.io)
- API Documentation: [Context.io API docs] (https://context.io/how-it-works/api-overview)

### Pre-Reqs
- you must install the com.soa.pso.policy.OAuth1.0.0.zip nto the <Policy Manager Home>/sm70 directory. This will result in files placed in the sm70/lib/soa-pso-policy-OAuth1.0.0 subdirectory
    + restart ND(s) only
    +  Using the SOA Admin Console, on each ND:
        * select the OAuth1 Token Policy Support feature  
        * press the "install" button
        * follow the install wizard instructions and restart the ND
- Register the application in the [Context.io Developers Console] (https://context.io/how-it-works/api-overview). Ensuring that you have registered and logged in.
- Click the "Accounts" tab, then the "add a Lite account" button, on the top right.
- follow the steps to define the email account your app/account will utilise
- once the account is defined, click on the "settings" tab, and the "API keys and Libraries" button.
- If you haven't already been asked, you'll be taken through the process of generating an App ID, App Key, and App Secret. If you have, the App Key, and App Secret will be displayed. Copy them for the set up of the security policy later.
- sign out of the console 

### Getting Started Instructions
#### Download and Import
- Download Context.ioLiteAPIHook.zip
- Download the migrations.properties file, and edit it to replace the <replace this with your key> text with the "Container Key" of the ND or ND cluster in your target PM.
    - the container key is found by going to the "Deatils Tab" of the ND cluster, or ND defined in the Policy Manager Console, then looking at the " Container Overview" tab on that page, and copying the "Container Key:" value. ![container key screenshot](https://github.com/pogo61/Google-Sheets-API-Integration/blob/master/Screen%20Shot%202015-03-18%20at%2011.24.45%20am.png "ND Container Key")
- Login to PolicyManager  example: http://localhost:9900
- Select the root "Registry" organisation and click on the "Import Package" from the Actions navigation window on the right side of the screen
  - click on button to browse for the Context.ioLiteAPIHook.zip archive file 
  - make sure select the migrations.properties file 
  - click Okay to start the importation of the hook.
- this will create a Context.io Lite API Hook Organisation with the requisite artefacts needed to run the API.

#### Verify Import
- Expand the services folder in the Context.io Lite API Hook you imported and find Context.io_Lite_API_Helloworld VS

#### Activate Anonymous Contract
- Expand the contracts folder in the Google Sheets API Hook you imported and find the "Anonymous" contract under the "Provided Contracts" folder
- click on the "Activate Contract" workflow activity in the righ-hand Activities portlet
- ensure that the status changes to "Workflow Is Completed"

#### Configure Security
- Go to Context.io Lite API Hook -> Policies -> Operational Policies ->    Insert OAuth 1.0 Token into Downstream Request policy
    - Click "modify" in the XML Policy Tab. An XML Policy Content editor dialog will be displayed.
    - change the value of the tns:secret element to be the secret you obtained in the Context.io developers console.
    - change the value of the tns:appKey element to be the value of the key you obtained in the Context.io developers console.
    - save the changes
    - click on the "Activate Policy" workflow activity in the righ-hand Activities portlet
    - ensure that the status changes to "State: Active"

#### Verify Connectivity
- Using curl http://"URL of the Listener of your ND"/contextio_hook/helloworld
-  the response should be similar to the below, listing your user details:  
    ```[
            {
                "created": 1426733556,
                "email_accounts": [
                {
                    "authentication_type": "password",
                    "label": "paulpog@japarasolutions.com::googleapps",
                    "port": 993,
                    "resource_url": "https://api.context.io/lite/users/550a39f5894615ab04d6f6db/email_accounts/paulpog%40japarasolutions.com%3A%3Agoogleapps",
                    "server": "imap.gmail.com",
                    "status": "OK",
                    "type": "imap",
                    "use_ssl": true,
                    "username": "paulpog@japarasolutions.com"
                }
            ],
            "email_addresses": [
                "paul.pogonoski@akana.com"
            ],
            "first_name": "Paul",
            "id": "550a39f5894615ab04d6f6db",
            "last_name": "Pogonoski",
            "resource_url": "https://api.context.io/lite/users/550a39f5894615ab04d6f6db"
        }
    ]
```


### How Hello World Works
#### An Akana Integration Primer
The Google_Sheets_API_Hook API is a "Virtual Service". That is, its interface is not that of a real service implementation. It can be a proxy to a "real" implementation, or it can be an aggregate (a combination) of a number of "real" implementations. In Policy Manager a "real" implementation is called a "Physical Service".
Apart from offering a different interface to the Physical Service, a Virtual Service offers the ability to attach Policies for security, logging, QoS, and a number of other non-functional capabilities.
Virtual Services also have the ability to have Custom Process and Scripts run before the Physical Service is called. Here is where a lot of the magic of Integration occurs.

#### Hello World
To create the helloworld operation the following was added to a base RAML document to create the context.io API Helloworld.raml document:  
    /helloworld:  
      &nbsp;get:  
        &nbsp;&nbsp;description: "returns all spreadsheets on your google drive"  
        &nbsp;&nbsp;&nbsp;responses:  
          &nbsp;&nbsp;&nbsp;&nbsp;200:  
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;body:  
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;application/atom+xml:  

Then a VS was created by using the RAML as the definition source.
Then the /helloworld Operation in the VS was mapped to the GET /users operation in the context.io_API_Hook PS.

Go to the Context.io_Lite_API_Helloworld VS -> Operations Tab -> GET /hellowworld operation -> Process tab you'll see this image:
![Helloworld process] 
(https://github.com/pogo61/Context.io-API-Hook/blob/master/Screen%20Shot.png)

Double click on the invoke activity to see how these work to make the Hello World operation call successful.


### Create Your Own Integration with the Context.io API
The Hello World operation is one simple way of integrating or extending your API's.
Take a look at the [Google Sheets API Integration](https://github.com/pogo61/Google-Sheets-API-Integration).
this will give you a deeper inderstanding of the richness of our gateway product in integrating to API's    

### Modify and Build
In the event you need to change the API Hook.   Here are the instructions to do so. 

### License
Put a link to an open source license

