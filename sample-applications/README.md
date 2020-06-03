# Recruiter System Connect Sample Applications

These are sample applications that allows you to plug in an API key and an integration context to see what the rendered widget looks like. 

## Getting Started

 Make sure to host the files in any webserver of your choice so you have a domain to whitelist. If you have Python installed, one very simple way of doing the same can be:

 From within your sample_applications folder run below command:
 - python -m SimpleHTTPServer 5000
 
 **For Partner ATS:**
 Make sure to whitelist the domain you are hosting on (for eg: http://localhost:5000) in the ValidJSSdkDomains field for Customer Application using the provisioning API.

 **For Customers:**
 Make sure to whitelist the domain you are hosting on (for eg: http://localhost:5000) by going to [LinkedIn Developer Portal](https://www.linkedin.com/developers/) and selecting your Development Application. You can whitelist(add) domains for Widget in the settings tab of your application. 

 ## Steps to see the ATS Integration Configuration Plugin

 ATS Integration Configuration Plugin is used for Customer OnBoarding workflow by Partner ATS.

Before deploying the applications in your webserver, please make sure to edit them 

1. Enter a valid API Key (CUSTOMER_APPLICATION_CLIENT_ID). Make sure that the same application has the current domain (http://localhost:5000) whitelisted.

2. Host your updated application (python -m SimpleHTTPServer 5000)

3. Enter below in your browser:
```
http://localhost:5000/ats-integration-configuration-plugin.html
```

4. Try out the widget by following the instructions in [ATS Integration Configuration Plugin Documentation](https://docs.microsoft.com/en-gb/linkedin/talent/middleware-platform/customer-configuration#2-display-the-ats-integration-configuration-plugin).

 ## Steps to see the Profile Widget

Before deploying the applications in your webserver, please make sure to edit them 

1. Enter a valid API Key (CUSTOMER_APPLICATION_CLIENT_ID). Make sure that the same application has the current domain (http://localhost:5000) whitelisted.

2. Enter a valid integration context received from the customer configuration plugin or shared via LinkedIn in a mail.

3. Enter an ATS Candidate ID for the candidate that is synced with LinkedIn Recruiter.

4. Host your updated application (python -m SimpleHTTPServer 5000)

5. Enter below in your browser:
```
http://localhost:5000/profile-plugin.html
```

6. Try out the widget. For more information refer [Profile PLugin Documentation](https://docs.microsoft.com/en-gb/linkedin/talent/recruiter-system-connect/profile-plugin).

## Running the demo
Goto your browser and enter (http://localhost:5000). You should see all HTML files listed (for eg: ats-integration-configuration-plugin.html, profile-plugin.html). You can select any of the HTML files to try out the widget they represent.

For eg:

```
http://localhost:5000/ats-integration-configuration-plugin.html
```

## Error handling

If the widget does not load or you have any errors prefilling the form please check the console for errors. Also when in the confirmation page, please check the console to make sure there are no errors trying to initialize the widget.

The error may look like:

```
Error trying to initialize the widget! Error is :<Error>
```

If you have any questions, you can reach out to us via Zendesk at https://linkedin.zendesk.com/hc/en-us.

