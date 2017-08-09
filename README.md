platform-events-acct-alerts
=======================

This project contains 2 apps:
- Node demo that publishes and subscribes to a Salesforce platform event.
(This node demo was based on this project: https://github.com/jthurst01/platform-events-rma.git)
- force.com app illustrating publishing and subscribing to an event on force.com and handling events from external sources.

### Setup Remote Access in Salesforce.com

Setup a new Connected App to get your OAuth tokens. For your callback,  use: http://localhost:3001/oauth/_callback

### Install Package for Platform Event Demo

You may install a package for the Account alerts demo at https://login.salesforce.com/packaging/installPackage.apexp?p0=04tf4000001KKE3.  
The package adds:
- one Platform Event definition and an after insert trigger that creates tasks in certain conditions.  
- a trigger on Case inserts that create Platform Events in certain conditions.
- a Lighting Record home page for Account that includes a Lightning Component that subscribes to the event. Use App Builder to set this page as the org default (or your preference in configuration).

Edit the config.js file so that the node app can connect to your Salesforce org and subscribe to the correct channel.
Find the index.hbs file under views and modify the list of Accounts to match your org.

### Running the Application Locally

```
git clone https://github.com/lcohensf/platform-events-acct-alerts.git
cd platform-event-acct-alerts
npm install
```

This will clone this repo locally. Then make the edits described above. Run the following to start the server:

```
node bin/www
```

Open your browser to  [http://localhost:3001](http://localhost:3001) and create an Account alert in Salesforce from the left hand form, and watch the stream of events as they are created in the right hand panel.
In the Salesforce app, navigate to the Account record that you are generating events for to see the events show up as notifications in the Lightning Component.
Set the VIP flag to true on an Account then test creating a High priority case for the Account.

### Source for the Force.com app

Source for the package is in the force_source folder. The app was defined as a managed package, therefore if you deploy the source rather than install the package, you will need to adjust the node routes to not use the namespace, pedemo.
