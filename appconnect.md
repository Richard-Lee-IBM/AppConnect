---

copyright:
  years: 2017, 2020
lastupdated: "2021-11-12"

subcollection: AppConnect

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# {{site.data.keyword.appconnect_notm}} concepts
{: #concepts}

{{site.data.keyword.appconservicefull}} helps you to connect your applications: from simple trigger-action interactions to complex integrations. You can use {{site.data.keyword.appconnect_notm}} to create event-driven flows or flows for APIs. Or you can upload and run the integration solutions that you create in IBM App Connect Enterprise or IBM Integration Bus, without the need to acquire and maintain an IT infrastructure. You can see and administer all your integrations - integration servers, event-driven flows, and flows for APIs - in one place on the {{site.data.keyword.appconnect_notm}} dashboard.
{: shortdesc}

The features and terminology of {{site.data.keyword.appconnect_notm}} are explained in more detail here:

-   [Flows](#flows)
-   [Applications](#apps)
-   [Actions](#actions)
-   [Data mapping](#transforms)
-   [BAR files and integration servers](#barfiles)

## Flows
{: #flows}

You can create two types of flow in {{site.data.keyword.appconnect_notm}}: an event-driven flow and a flow for an API.

In an event-driven flow, you identify an event that can occur in your first application (the source application), and actions that can be performed in one or more target applications. The flow links the event to the actions so that, whenever the event occurs in the source application, the action is automatically triggered in the target applications. Each successfully completed action counts towards your monthly quota. When you create a flow, you add your applications, and choose actions. Then, you map the data that you want to transfer between your applications.

For example, you might create a flow so that whenever someone registers as a new attendee with Eventbrite (the event), {{site.data.keyword.appconnect_notm}} automatically retrieves details of the attendee from Salesforce and creates a task in Asana (the actions).

![A multi-node flow, with the source application and two target applications](images/multi_node_flow2.jpg)

For more information, see [Creating an event-driven flow ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/en/SS6KM6/com.ibm.appconnect.dev.doc/tutorials/creating-event-driven-flow.html).

A flow for an API contains a request, one or more target application actions, and a response. The request uses a model that you define to request the creation, replacement, or retrieval of data objects in your applications. When the request is submitted, each target application performs its action.  The flow then returns a response that either confirms that the actions were successful, or returns the data that was requested.

![A flow for an API that creates a product in Salesforce](images/APIFlow2.jpg)

For more information, see [Creating flows for an API ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/en/SS6KM6/com.ibm.appconnect.dev.doc/tutorials/creating-flows-api.html).

As well as adding applications to your flows, you can also add nodes from the **Toolbox** to configure how you process data. For example, use the "If" node to add some conditional processing - performing different actions according to the data that you receive (see [Adding conditional logic to a flow ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/en/SS6KM6/com.ibm.appconnect.dev.doc/toolbox/conditional-logic-flow.html)). Or use the "**For each**" node when you want to perform an action for each record that is returned by a retrieval action (see [Retrieving items from your applications ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/en/SS6KM6/com.ibm.appconnect.dev.doc/tutorials/retrieve-items-applications.html)).

If you're an App Connect Enterprise or IBM Integration Bus developer, you can also create complex integration solutions by developing message flows in the Integration Toolkit and packaging them into BAR files.

Your flows and integration servers are represented by tiles on the App Connect dashboard. The tiles show summary information about the flow, API, or integration server, such as whether a flow is running or stopped, and if it produced an error. You can click the tick and exclamation point icons to see when the flow last ran successfully, or what errors were raised. Click the three dots ![Icon of three vertical dots opens a menu to start, stop, edit, or delete the flow](images/Menu.jpg) to open a menu to start, stop, edit, or delete your resources. Flows have to be stopped before you can edit them.

![Screen capture that shows tiles from the dashboard for event-driven flows, flows for APIs, and integration servers](images/Dashboard.jpg)

## Applications
{: #apps}

When you create event-driven flows or flows for APIs, _applications_ are the cloud-based software applications that you're connecting.  You can see a list of the applications that you can connect with {{site.data.keyword.appconnect_notm}} on the **Applications** page of the catalog. Click an application to find out more about it, to see what events and actions are supported, and to connect to your own account. You can connect multiple accounts to each application and switch between them on the Applications page. After you connect to your account, you can also update or remove your account on the Applications page.

![Screen capture of one of the applications on the Applications page](images/Magento2.jpg)

You don't have to connect to your applications on the Applications page; you can also connect in the flow editor as you add the applications to your flow. Many applications require just a user name and password, but some need more information. You can find out how to find this information in the [How-to guides for apps ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/en/SS6KM6/com.ibm.appconnect.dev.doc/how-to-guides-for-apps/index.html).

If you're using {{site.data.keyword.appconnect_notm}} to run BAR files in the cloud, an _application_ is the container that holds message flows, libraries, and other resources that are required by your solution.

## Actions
{: #actions}

You can add several types of action to your flows. Common actions include create, retrieve, update, and delete, but some applications have specific actions. For example, the Watson Personality Insights application has an action that is called "Analyze personality". You can see a list of applications that an action can be performed on {{site.data.keyword.appconnect_notm}} by typing the action type in the search field on the Applications page:

![Screen capture that shows supported retrieval actions for applications](images/RetrieveApps2.jpg)

### Create
{: #create}

As the name suggests, the create action creates an object or record in an application. For example, if someone signs up to your event or submits a completed form, you might want to create a record for that person in your CRM or marketing application. Or if someone opens a ticket in your help desk application, you might want to create an email or instant message to ensure that someone deals with it straight away. If the object that you want to create might exist, you can use an *update or create* action instead.

For some applications, you might have to provide some extra information when you add a create action to a flow so that your flow knows where to create the object. For example, if you're using a project management application like Asana or Trello, you need to specify a project or board when you create a task or a card.

### Update or create
{: #update_create}

The update or create action changes an existing record in your target application if it exists, but creates the record if it doesn’t exist. It is also known as an upsert (update or insert) action.

For example, say that someone submits a Wufoo form with a change of address. If the contact is already in your CRM system, you want to update their address; but if they’re not, you want to add them. When you choose an action to update data in one of your applications, you can add one or more conditions to ensure that you’re updating the right information.

If there’s more than one record in your target system that matches your criteria, you see an error for the flow on the dashboard.  In this case, the flow doesn’t update or create any records. For example, maybe you have more than one contact with the same first name and surname. So you could try to match a contact by using unique data, such as their email address.

You're likely to see the following status codes in response to an update or create action.
-   200 A record was updated
-   201 A record was created

You can use these response codes later in your flow. Maybe you want to take different actions that depend on whether a record was updated or created. For an example of defining actions based on response codes, see the tutorial [Updating or creating a contact in Salesforce and updating Asana when a Wufoo form is submitted ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/en/SS6KM6/com.ibm.appconnect.dev.doc/tutorials/create-contact-salesforce-updates-asana-whenever-receive-form-wufoo.html).

### Retrieve
{: #retrieve}

The retrieval action gets information from an application so that you can use it in another application.

When you add an action to your flow to retrieve objects, you can define one or more conditions to make sure that you’re retrieving the right items. Or, if you want to retrieve all items of a particular type, you can delete the condition. You can also define how many items you want to retrieve, and what happens if {{site.data.keyword.appconnect_notm}} finds more than or less than that number.

You can handle your retrieved items in two ways:
-   You can add a "For each" node after the retrieval action to perform an action for each of the items that were retrieved.
-   You can add another action after the retrieval action to process the list of retrieved items. This action is a single action, no matter how many items are returned – such as creating an email that lists all the retrieved items.

You can also decide what action to take based on the status code that you get in response to the retrieval action. You could use an “If” node to perform different actions for different status codes. You're likely to see the following status codes in response to a retrieval action are.
-   204 No records were found
-   200 All records in the application match the condition
-   206 The specified maximum number of records were retrieved, but more matching records exist in the application

For more information, see [Retrieving items from your applications ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/en/SS6KM6/com.ibm.appconnect.dev.doc/tutorials/retrieve-items-applications.html).

## Data mapping
{: #transforms}

After you create a flow, add your applications, and select appropriate actions, you must specify what information you want to transfer between your applications. You can see in the flow editor that when you add an action to your flow, you see a list of available fields for that application.  You can populate these fields with data from your source application, or previous actions in the flow.

Some fields are mandatory, and they're marked with an asterisk. For example, when you're creating a lead in Salesforce, you must specify a surname:

![Screen capture that shows that the "Last name" field is mandatory](images/LastName.jpg)

When you click in one of these fields, you see a couple of icons: **Insert a mapping** ![Insert a mapping icon](images/InsertRef.jpg) and **Insert a function** ![Insert a function icon](images/Functions.jpg). If you click **Insert a mapping**, you can see the available data that you can put in that field from preceding applications in the flow. The following example shows that you can choose fields from the Wufoo source application, or from a previous Salesforce action in the flow. You can also use the status code from the Salesforce update or create action.

![Screen capture that shows available inputs for a data mapping](images/Inputs.jpg)

In the following example, the flow is triggered when a new completed form is received in Wufoo. You want to create a contact in Salesforce for the person who submitted the form. So when you add your Salesforce "Create contact" action to the flow, you copy the details for your contact from the Wufoo form. Here you can see that for the surname of the Salesforce contact, you select the surname of the Wufoo form submitter. You can see that the mapped field is from Wufoo because of the color:

![Screen capture that shows that the Wufoo "Last name" field is mapped to the Salesforce "Last name" field](images/Mapping.jpg)

In the following example, you add a Slack "Create message" action to the flow after a Salesforce "Update or create contact" action. You want to put a message on Slack to say what response code is received for the Salesforce action:

![Screen capture of a Slack Create message action that maps a response code](images/SlackSC.jpg)

You can see that in the **Text** field for the Slack "Create message" action you type a message, then map in the status code for the Salesforce "Update or create contact" action.

Here's another example of mapping response codes in a different way. This time, you add an "If" node after a Salesforce "Update or create contact" action.  The "If" node performs different actions that depend on whether an existing Salesforce contact is updated, or a new contact is created. In this case, a response code of "200" means that the contact is updated. So this branch of the "If" node contains an action that's specific to an updated record.

![Screen capture that shows how response codes are used in an "If" node](images/IfSC.jpg)

The **Insert a function** icon ![Insert a function icon](images/Functions.jpg) shows you a list of transformation functions that you can use to customize the data that you're passing through your flow. These functions can be as simple as converting a particular field to uppercase or lowercase text, or slightly more complex, such as finding and replacing specific patterns in the data. They can also be as powerful as forming regular expressions. You can either select the function that you want from the list, or you can type it in yourself. The syntax of the functions is JSONata (a lightweight query and transformation language). For more information, see [http://jsonata.org ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://jsonata.org).


## BAR files and integration servers
{: #barfiles}

A BAR file is a compressed file to which you add deployable resources in App Connect Enterprise or IBM Integration Bus.  When you develop an integration solution in App Connect Enterprise or Integration Bus, you package your message flows and all the resources that those message flows use in a BAR file.  You then deploy the BAR file to an integration server.  That server can be on premises or in {{site.data.keyword.appconnect_notm}}.  You can run your App Connect Enterprise or Integration Bus solutions in App Connect, without the need to acquire and maintain an IT infrastructure.  When you upload a BAR file to App Connect, an integration server is created to run the contents of the BAR file.  You can configure basic authentication and secure connectivity between your cloud-based and on-premises resources (see [Running enterprise integration solutions in App Connect on IBM Cloud ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SSTTDS_11.0.0/com.ibm.ace.cloud.doc/index.html)).  
