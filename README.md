# Akana API HOOK
![Image of Akana] 
(https://www.akana.com/img/formerlyLOGO8.png) 
[Akana.com](http://akana.com)

## Context.io API Integration
### About the API
- This API returns the Contents (in HTML format) of the first email, of the first folder, of the first email account found in your Context.io account.
- Home Page: [Context.io] (https://context.io)
- API Documentation: [Context.io API docs] (https://context.io/how-it-works/api-overview)

### Pre-Reqs
- You must have installed and verified, via the HelloWorld integration, the Context.io API Hook. 

### Getting Started Instructions
#### Download and Import
- Download Context.ioLiteAPIIntegration.zip
- Download the migrations.properties file, and edit it to replace the <replace this with your key> text with the "Container Key" of the ND or ND cluster in your target PM.
    - the container key is found by going to the "Deatils Tab" of the ND cluster, or ND defined in the Policy Manager Console, then looking at the " Container Overview" tab on that page, and copying the "Container Key:" value. ![container key screenshot](https://github.com/pogo61/Google-Sheets-API-Integration/blob/master/Screen%20Shot%202015-03-18%20at%2011.24.45%20am.png "ND Container Key")
- Login to PolicyManager  example: http://localhost:9900
- Select the root "Registry" organisation and click on the "Import Package" from the Actions navigation window on the right side of the screen
  - click on button to browse for the Context.ioLiteAPIIntegration.zip archive file 
  - make sure select the migrations.properties file 
  - click Okay to start the importation of the hook.
- this will create a Context.io Lite API Integration Organisation with the requisite artefacts needed to run the API.

#### Verify Import
- Expand the services folder in the Context.io Lite API Integration you imported and find Context.io_API_Integration VS

#### Activate Anonymous Contract
- Expand the contracts folder in the Google Sheets API Hook you imported and find the "Anonymous" contract under the "Provided Contracts" folder
- click on the "Activate Contract" workflow activity in the righ-hand Activities portlet
- ensure that the status changes to "Workflow Is Completed"

#### Configure Security
- Nil.

#### Verify Connectivity
- Using curl http://"URL of the Listener of your ND"/contextio_int/mail
-  the response should be similar to the below, listing of the first email, of the first folder, of the first email account found in your Context.io account:  
    ```{"status":"Success", "detail":"
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"
"http://www.w3.org/TR/html4/loose.dtd">
<html lang="en">
    <head>         
        <meta http-equiv="Content-Type" content="text/htzml; charset=utf-8">     
        <meta name="viewport" content="width=device-width, initial-scale=1.0">     
        <meta http-equiv="X-UA-Compatible" content="IE=edge">         
        <title>Tackle &amp; Track Your Goals in Evernote</title>        
            <style type="text/css">
            ...............
            </style>     
    </head>     
    <body bgcolor="#FFFFFF" style="-webkit-font-smoothing: antialiased; width:100%;background:#ffffff;-webkit-text-size-adjust:none; margin:0; padding:0;">.....................
    </body>
</html>
"}
```   

### Modify and Build
In the event you need to change the API Hook.   Here are the instructions to do so. 

### License
Put a link to an open source license

