# Workshop 2 Watson Conversation Service

## Architecture
Below is the architecture overview of workshop 2, the Watson Conversation Service (WCS). This architecture
is consistent with the reference implementations of WCS for cloud native applications using microservices.
![Architecture Overview](/images/wk2-arch-overview.png)


## Application Overview
Workshop 2 is intended to help you understand the basics of the Watson Conversation Service (WCS)
as part of the Watson API's. WCS is a question and answer system that focuses on providing
a dialog type of experience between the user and the conversation system. This style of interaction
is commonly called a bot. The intent of this lab is to take the base work model from workshop 1
and extend the lab to leverage the WCS capabilities. We will enable through a dialog approach
WCS interacting with the data from the IoT device, asking questions specific to the data that is
captured. The lab will also allow for commands to be sent to the IoT device, directed from the
response of the WCS dialog flow. Though the example is simple, it will provide you with a 
solid understanding of the core pieces of WCS.

### Terminology
WCS has a couple of terms that need to be understood. This will allow for an easier time with
creating an application (i.e. Dialog) in WCS

**Intent:** An intent is the intention of the command or question given by the user to WCS.
	It is common to think of intents as the verbs or actions that need to occur. An Example of
	an Intent is "Tell me the temperature" or "I want to know the current temperature". In both
	cases, though the sentences are different they both as asking WCS for temperature information.
	It should be noted that WCS can only support a single Intent per interaction with WCS. So 
	asking questions with multiple intents will produce unreliable ordering of answers to the question.
	
**Entities:** An entity is the object that intents use to help narrow the scope of the request.
	It is common to think of entities as nouns or objects. The nice thing about entities, compared to
	intents, is that you can have multiple entities per interaction. This is very helpful when trying
	to narrow down the answers to a question. 
	
**Dialog:** The conversation that is created within WCS, is called a dialog. A dialog is 
	composed of creating a flow between intents and entities. The combination of flows and
	subFlows allows WCS to provide mult-layered conversation based on multiple interactions, 
	instead of a single question and answer. 
	

## Project Repositories

## Workshop Setup

## Workshop Instructions
Below are the steps for workshop 2

### Steps
1. Create a Watson Conversation Service instance
	1. Logon to BlueMix and go to your dashboard.
	2. Click on the catalog button at the top navigation on the right
	3. Select "Watson" on the left navigation under the Services menu
	4. Click on "Conversation"
![Architecture Overview](/images/wk2-catalog-wcs.png)	 
	5. In the service name type STSA-WK2-WCS-xxx (where xxx is your team number). You can leave credential name as is if you like
	6. Click on the create in the lower right corner.
	You should now see the following
![Architecture Overview](/images/wk2-wcs-manage.png)
	7. You will need cut and paste your service credentials. Click on "Service Credentials"
	on the left navigation, right under "Manage". Once the page has loaded, click on "View Credentials" on the right side of the screen.
	A drop down will show with your specific credentials
![Architecture Overview](/images/wk2-wcs-credentials.png) Your values for username and password will be different than shown.
	8. Click the copy icon to copy the values to your clipboard. Paste the values in a text file for later use.
	9. Go back to the manage page, by clicking on the manage link on the left side navigation. This will take you back to the manage page.
	
You have now completed the first step in creating the WCS service instance.

2. Launch WCS tooling
	1. Click on the "Launch tool" icon to take you to the WCS workspace
![Architecture Overview](/images/wk2-wcs-manage-launch.png)
	2. This will open another browser window and you should now be on the Watson Conversation Workspace page
![Architecture Overview](/images/wk2-wcs-workspaces.png)
	3. You are going to create a new workspace. Click on the "Create a new workspace" tile.
	4. Enter a workspace name i.e. STSA-WK2-xxx (where xxx is your team number).
	![Architecture Overview](/images/wk2-wcs-workspaces-create-popup.png)
	5. You are now ready to create some **Intents**. Click on the Intents link. You should now see the following:
	![Architecture Overview](/images/wks-wcs-workspaces-create-intents.png)
	Click the "Create New" button in the middle of the page. You should now see the following:
	![Architecture Overview](/images/wk2-wcs-workspaces-intents-add.png)
		1. Add a new Intent name of **Information**. You then need to provide some examples. Look at the image below and copy the samples provided.
		![Architecture Overview](/images/wk2-wcs-workspaces-intents-examples.png)
		2. Add another intent, by clicking "Create new" button. Use the new Intent name of **Greeting**. Look at the image below and add the examples.
		![Architecture Overview](/images/wk2-wcs-workspaces-intents-greeting.png)
		3. Add another intent **GoodBye**. Add the following examples also.
		![Architecture Overview](/images/wk2-wcs-workspaces-intents-goodbye.png)
		4. Add one last intent **ChangeColor** with the following examples:
		![Architecture Overview](/images/wk2-wcs-workspaces-intents-changecolor.png)
		You have now finished creating all of the intents.
		
	6. Next we want to create some **Entities**. Click on the "Entities" link at the top of the page.
	![Architecture Overview](/images/wk2-wcs-workspaces-entities-add.png)
	Click the "Create New" button. 
		1. Type "Temperature" as the new Entity name.
		![Architecture Overview](/images/wk2-wcs-workspaces-entities-examples.png)
		Now notice, you need to add examples of new "Temperature" entities. So add **"Current Temperature"** as a new entity 
		but also you need to provide some synonyms to help identify variations of the entity value. Now add **"Temperature now"** and **"Current Temp"** 
		as synonyms. You now need to add **"Average Temperature"** and **"Temperature"** with the corresponding
		 synonyms, as shown in the image.
		2. Create another entity called "degree" also add the associated synonyms.
		![Architecture Overview](/images/wk2-wcs-workspaces-entities-degree.png)
		3. Add one last entity called **Colors** and the associated values.
		![Architecture Overview](/images/wk2-wcs-workspaces-entities-colors.png)
		
	7. We are now ready to create a dialog. Click on the Dialog link at the top of the page.
	![Architecture Overview](/images/wk2-wcs-workspaces-dialog-add.png)
	Click the "Create" button to start to create a dialog. You should now see the following:
	![Architecture Overview](/images/wk2-wcs-workspaces-dialog-start.png)
	What you see are two "Dialog Nodes". The first is the standard "Welcome" message and the other
	is a catch-all "Anything else" . Remember the way a conversation dialog works, by scanning from the top of the tree
	and evaluating every node until a condition is met that satisfies the question being asked. So when the conversation starts
	WCS will respond with the "Welcome" Node. If you click on the "Welcome" node you will see that the standard Watson response
	is "Hello. How can I help you?"
	8. We now want to create our own node, based on the "Intents" we create earlier. To add a new node in the tree, below the "Welcome"
	node, click on the "Plus" icon, below the "Welcome" node.
	![Architecture Overview](/images/wk2-wcs-workspace-dialog-node-add.png)
	You should now see the following:
	![Architecture Overview](/images/wk2-wcs-workspaces-dialog-add-input.png)
		1. We are going to add some very simple nodes. Type **Greeting** as the name of the node. The trigger should be **"#Greeting"**. The Response condition should be set to "True" and you can provide any response text you like. It should look similar to the following:
		![Architecture Overview](/images/wk2-wcs-workspaces-dialog-node-greeting.png)
		1. Again create another root node by clicking the "Plus Sign" under the "Greeting" node. This will add another node. This nodes values are as follows:
		![Architecture Overview](/images/wk2-wcs-workspaces-dialog-node-goodbye.png)
		1. Create a new node under the "Goodbye" node, called **Color Change** with the following information:
		![Architecture Overview](/images/wk2-wcs-workspaces-dialog-node-colorchange.png)
		Take special note of the extra information in the first response. Make sure to copy it properly. 
		`<? entities.Colors.literal ?>` is an expression langage snippet of code. If you look at the information in the node, the intent is to change color and the first condition for a response is "@Colors", which
		signals to Watson, if a known color is provided in the user's input then use that color in the response. If an unknown color is typed (i.e. Violet) in the user's input the processing will hit the "True" condition. This is because "Violet" is not in our "@Color" entity definition.
		1. Create a node under "Color Change" called **WhatElse**, with the following information:
		![Architecture Overview](/images/wk2-wcs-workspaces-dialog-node-whatelse.png)
		
		1. We are now on the last node we are going to create. Insert this node between the "Goodbye" and "Color Change" node. This is done by clicking on the 
		goodbye node and then clicking the "Plus Sign" underneath it. 
		![Architecture Overview](/images/wk2-wcs-workspaces-dialog-node-aftergoodbye.png)
		
		2. Enter "Information" as the name of the node. In the Trigger field type the word "Information" you will see a type ahead pop up. Select the "#Information" entry. **Do not provide any responses.**
		![Architecture Overview](/images/wk2-wcs-workspaces-dialog-node-information.png)
		4. Click the large green X at the top to close the dialog editor.
		5. Now you want to create a sub-dialog. This time click on the "Plus Sign" to the right of the "Information" Dialog node.
		![Architecture Overview](/images/wk2-wcs-workspaces-dialog-node-information-plussign.png)
		6. Enter "Temperature" as the name of the node.
		7. In the Trigger field enter "@Temperature:(Current Temperature)". This is the entity defined earlier.
		![Architecture Overview](/images/wk2-wcs-workspaces-dialog-node-information-temperature.png)
		8. In the Response section, for the first response, add a response condition. Type "@degree:Celsius" in the response condition field.
		Then add the Watson response of "The current temperature in celsius is"
		9. Add another response condition of "@degree:Fahrenheit" with the response message of "The current temperature in fahrenheit is".
		10. Add one last response condition of "True". this is a catch all condition for this node. Add the Watson response as "The current temperature in fahrenheit is"
		The reason for this last response to have a response in the event Watson knows you are looking for information about the temperature, but isn't sure if you mean in celsius or fahrenheit.
		Your completed node should look the like the following:
		![Architecture Overview](/images/wk2-wcs-workspaces-dialog-node-temperature.png)
		Close the node editor, we have one last sub-node to create.
		11. Under the "Temperature" node, create a new node. Call it **Unknown** Add the information like below:
		![Architecture Overview](/images/wk2-wcs-workspaces-dialog-node-information-unknown.png)
		12. The next step is to go back to the "Information" node, by clicking on the node itself. You need to edit the node, so click on the green pencil icon.
		![Architecture Overview](/images/wk2-wcs-workspaces-dialog-node-information-plussign.png)
		Once the node editor is open, look at bottom right corner. There is a button "Wait for user input". Click on the button, we want to change the behavior of the "Information" node, from waiting for user input to "Jump to" a node.
		Click the **Jump To** option. The screen will change, select the "Temperature" node, which is a sub-node of "Information". 
		![Architecture Overview](/images/wk2-wcs-workspaces-dialog-node-information-jump.png)
		You will then see an option for "Go to condition" and "Go to response". Select **"Go to condition"** 
		"Your screen should look like the following:
		![Architecture Overview](/images/wk2-wcs-workspaces-dialog-node-information-jump-condition.png)
		13. Next we want to select the green pencil on the "Temperature" node. Like with the "Information" node, select the "Wait for user input" button and click **Jump to**.
		Then select the **"WhatElse"** node. This time select the "Go to response" option. The sub-flow should now look like the following:
		![Architecture Overview](/images/wk2-wcs-workspaces-dialog-node-information-temperature-jump.png)
		13. Next we want to select the green pencil on the "Temperature" node. Like with the "Information" node, select the "Wait for user input" button and click **Jump to**.
		Then select the **"WhatElse"** node. This time select the "Go to response" option. The sub-flow should now look like the following:
		![Architecture Overview](/images/wk2-wcs-workspaces-dialog-node-information-temperature-jump.png)
		14. Click the three bubbles in the upper right on the Temperature node by the responses
		![Architecture Overview](/images/wk2-wcs-workspaces-dialog-node-temperature-json.png)
		Then click on the **JSON** menu item.
		![Architecture Overview](/images/wk2-wcs-workspaces-dialog-node-temperature-json-pulldown.png)
			1. We are going to add a single line of code to the JSON. The purpose of this code, is to send a signal to the NodeRed application that some special processing needs to occur.
			So for the response to the **degree:Celsius** entity needs to have a new attribute on the JSON object. Type **"action": "CurrentTempCelsius"** make sure you put the "semicolon" right after the curly bracket, but before the new code you just added.
			![Architecture Overview](/images/wk2-wcs-workspaces-dialog-node-temperature-json-celsius.png)
			2. You now need to do the same thing for the each of the other responses on the temperature node. 
			For the **degree:Fahrenheit** response add **"action": "CurrentTempFahrenheit"**
			![Architecture Overview](/images/wk2-wcs-workspaces-dialog-node-temperature-json-fahrenheit.png)
			3. Now do it for the **True** condition as well. We will have the default response be in fahrenheit so add **"action": "CurrentTempFahrenheit"** 
			![Architecture Overview](/images/wk2-wcs-workspaces-dialog-node-temperature-json-default.png)
		15. The last step is to update the **ChangeColor** dialog node, with a similar action command. but this time set the command value to **"action":"changeColor"**
		![Architecture Overview](/images/wk2-wcs-workspaces-dialog-node-changecolor-json.png)
		We are now finished with the entire Dialog. Congratulations. We will be coming back here to make a couple of minor updates. Now is time to test your code.
	9. Deploy the NodeRed Flow . What might become obvious is that the responses from WCS are static. There is nothing personalized in the responses.
	Because of this we need to add a layer in front of WCS to take the responses and make them personalized. We are going to use NodeRed, like we did for the IoT lab.
	Below are the steps needed for adding a new flow to your existing **BlueMix NodeRed** application.
		1. Open your browser and go to the BlubMix NodeRed URL. It should be something like STSAWorkshops-xx.mybluemix.net. You can also get to it from your BlueMix Dashboard.
		2. Login to your NodeRed Editor
		![Architecture Overview](/images/wk2-nodered-logon.png)
		3. You should now see something like the following, which is your flow for IoT
		![Iot Flow](/images/wk2-nodered-flow-iot.png)
		4. Go to the following URL https://github.com/jdcalus/STSA-Workshop-2-WCS 
		You should see something similar to the following:
		![Iot Flow](/images/wk2-github-home.png)
		5. Click on the wk2-wcs-flow.json link. This will take you to the NodeRed flow json file which has a predeveloped flow for talking to WCS. You should now see:
		![Iot Flow](/images/wk2-github-flowjson.png)
		6. Highlight all of the json text and copy it to your clipboard. (ctrl+c on your keyboard).
		7. Go back to your NodeRed editor and in the upper right corner is the cake layer icon, click on it. Then click import and then click clipboard
		![Iot Flow](/images/wk2-nodered-import.png)
		8. You should now see the following dialog window:
		![Iot Flow](/images/wk2-nodered-import-paste.png)
		click in the center of the dialog and paste the information from your clipboard. (ctrl+v). Make sure the **new flow** button is pressed before you import.
		Your screen should now look something like the following, which a new tab called **WCS Flow**
		![Iot Flow](/images/wk2-nodered-flow-wcs.png)
		9. Now we need to update a couple of the nodes, with information that was provided earlier in IoT Workshop.
			1. Make sure you have the credentials information from your DashDB service. This can be access from your BlueMix dashboard, by clicking on the service:
			![Iot Flow](/images/wk2-bluemix-dashboard-dashdb.png)
			You should see the manage page for that instance of the dashDB service
			![Iot Flow](/images/wk2-bluemix-dashdb-manage.png)
			Now click on the Service Credentials link on the left side. Once the page loads, there is an option for **View Credentials**.  You will need to copy the **HostName, Username and Password** in the next step.
			![Iot Flow](/images/wk2-bluemix-dashdb-credentials.png)
			2. Now go back to NodeRed and make sure you are in the WCS flow.
			Click on the Current Temp node. This is a DashDB node, so we need to make sure the setting are configured properly. You should see something like:
			![Iot Flow](/images/wk2-nodered-flow-wcs-dashdb-config.png)
			Click on the pencil icon to set up the connection information. You should see something like
			![Iot Flow](/images/wk2-nodered-flow-wcs-dashdb-blank-security.png)
			Once you fill in the values it should look similar to:
			![Iot Flow](/images/wk2-nodered-flow-wcs-dashdb-security.png)
			Click the **update** button then click on the **Done** button. Your dashDB node should now have the proper information to connect to the service instance.
			3. Now double click on the **IoT Change Color** node.
			![Iot Flow](/images/wk2-nodered-flow-wcs-iotdb.png)
			We need to make sure the connection information is correct. Like from workshop 1, enter the appropriate values.
			4. The final step is to double click on the **STSA-CONV** node. 
			![Iot Flow](/images/wk2-nodered-flow-wcs-iotdb.png)
			This is the Watson Conversation node, that connects to the conversation you just created above.
			![Iot Flow](/images/wk2-nodered-flow-wcs-iotdb.png)
			Provide the **Username, password and Workspace** values from above.
			Click **Done** when completed.
			You are done updating the NodeRed Flows for WCS
			Click the **DEPLOY** button at the top of the screen.
			
		10. The next step is to create a sample application that connects to your NodeRed flow. When you click on the button below, you will be taken to bluemix DevOps page. This will automatically create a new application for you, via the DevOps ToolChain. If you are not logged on to BlueMix you will need to logon.
		[![Deploy to Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/jdcalus/STSA-WCS-WebProxy.git)
		
		You will see a screen like the following:
		![Iot Flow](/images/wk2-devops-autocreate.png)
		Click the deploy button, after about 1 minute or less, your screen will change to something like the following:
		![Iot Flow](/images/wk2-devops-toolchain-autocreate.png)
		Click on the **Deliver** tile
		![Iot Flow](/images/wk2-devops-toolchain-deliver-icon.png)
		Then you should see something like the following:
		![Iot Flow](/images/wk2-devops-toolchain-deliver-home.png)
		Once the message in the deploy tile has changed to finished from Deploy running, click on the **Last Executed Results**
		![Iot Flow](/images/wk2-devops-toolchain-deliver-deploy-tile.png)
		This will take you to the newly created applications. Your screen should now look like:
		![Iot Flow](/images/wk2-bluemix-wcs-webclient.png)
		Click on the **Runtime** link on the left and your screen should change, then click on environment tab in the middle of the screen. It should look like the following:
		![Iot Flow](/images/wk2-bluemix-wcs-webclient-runtime.png)
		In the **CONVERSATION_URL** value change the "xxxxxx" to the hostname of your **NodeRed** application. This comes from the NodeRed url that where you are creating your NodeRed flow. So something like "STSAWorkshops-xx.mybluemix.net", do not include "/red/#	
		Click the **Save** button. The application will restart.
		Click on the **Visit App URL**. This is at the top of the page. You will get an error message. That is okay. You need to add **webclient** to the end of the browsers URL.
		![Iot Flow](/images/wk2-bluemix-wcs-webclient-url.png)
		Your screen should now look like the following:
		![Iot Flow](/images/wk2-bluemix-wcs-webclient-webpage.png)
		
		11. You can now ask Watson questions about the temperature.
			1. What is the current temperature in Celsius
			2. What is the temperature
			3. What is the current temperature in fahrenheit
			4. Change the background color to blue

### This concludes the Workshop 2
	
## Toolchain Installation
In the event you are not able to complete the workshop in enough time, we have provided a
DevOps toolchain that will allow for you to quickly get a completed lab setup. Follow the
instructions below to install a completed workshop 2 within BlueMix.

### Steps
