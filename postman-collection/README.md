# How to use Postman Collections
The easiest way to get started using the Recruiter System Connect APIs is to use our Postman collections. <br>Postman is a free-to-download tool for making HTTP requests. You can find more details about Postman [here](https://www.postman.com).<br>
The following steps outline the necessary actions in order to install Postman and gain certainty that everything is working as it should be.
<br>If you prefer, you can explore our API with other tools like curl.

[IMPORTANT] PLEASE NOTE THAT POSTMAN IS AN INDEPENDENT ENTITY AND IS NOT AFFILIATED WITH LINKEDIN. LINKEDIN IS PROVIDING THE FOLLOWING RESOURCES TO SUPPORT YOUR USE OF THE POSTMAN SERVICES BUT ULTIMATELY, ANY USE OF THIRD PARTY SERVICES, SUCH AS THE POSTMAN SERVICES, IS AT YOUR OWN DISCRETION AND RISK. LINKEDIN DOES NOT ENDORSE OR VET THE POSTMAN SERVICES AND IS NOT RESPONSIBLE FOR ANY DAMAGE OR LOSS OF DATA RESULTING FROM YOUR USE OF THIRD PARTY SERVICES. NOTHING HEREIN SHALL RESTRICT LINKEDIN'S ABILITY TO ENFORCE ALL OF ITS RIGHTS UNDER ITS AGREEMENTS WITH YOU.

## Install Postman
Visit www.getpostman.com and download the version of Postman required for your platform and complete Postman installation.

## Import Postman Collection

- Open Postman
- Click the `Import` button, click the `Choose Files` button and locate the required collection JSON file to import. An import success message appears for each collection imported and then you can see the collection in the `Collections` tab.
- After a collection is successfully imported into postman, Click `...` icon next to an imported collection and click on the `Edit` button to setup variables.
- Please set the value for the variables and click on the `Update` button.
- You have successfully setup and are now ready to make API calls.

## Recruiter System Connect Postman Collection Variables

|Variable Name|Description|
|---|---|
|partner_app_client_id|Client id of Partner's Application. It will be used to get the access token to be able to call `Provision Customer Application` APIs|
|partner_app_client_secret|Client secret of Partners Application. It will be used to get the access token to be able to call `Provision Customer Application` APIs|
|customer_app_client_id|Client id of Customer's Application. It will be used to get the access token to be able to call `Middleware Platform` APIs (For syncing data from ATS to LinkedIn or retrieving data from LinkedIn)|
|customer_app_client_secret|Client secret of Customer's Application. It will be used to get the access token to be able to call `Middleware Platform` APIs (For syncing data from ATS to LinkedIn or retrieving data from LinkedIn)|
|org_id|The organization(company) 'id' value for Customer. This appears in `integration_context` of type 'urn:li:organization:id'. For Partner ATS with multiple Customers, this value is obtained when the customer requests for `Recruiter System Connect` integration using `ATS Integration Configuration Plugin`|
|contract_id|The contract 'id' present in contract urn of type 'urn:li:contract:id'|
|customer_name|Name of the Customer|
|unique_foreign_id|Unique ID used to discover customer in partner ATS|
|candidate_id|Unique ID of Customer in ATS that needs to be synced to LinkedIn. This will help in quickly trying POST, GET calls|
|note_id|Unique ID of Candidate Note for the customer in ATS that needs to be synced to LinkedIn. This will help in quickly trying POST, GET calls|
|application_id|Unique ID of Job Application for the customer in ATS that needs to be synced to LinkedIn. This will help in quickly trying POST, GET calls|
|private_externalJobPostingId|Unique ID of Job being posted with availability type as 'private' in ATS.his will help in quickly trying POST, GET calls|
|public_externalJobPostingId|Unique ID of Job being posted with availability type as 'public' in ATS.his will help in quickly trying POST, GET calls|

> [!NOTE]
>
>For Customers who have a proprietory ATS platform, "Module 1 - Configure Customer Middleware Integrations (Partner Only )" APIs should NOT be executed. Hence, customers need not set any value for fields: 'partner_app_client_id', 'partner_app_client_secret', 'customer_name' and 'unique_foreign_id' in Postman Collection variables.


## How to get Access Token to Execute APIs

Once you have edited the Postman collection & provided values for the global variables, you can start trying out any API. Before executing the APIs you need to get two access tokens:

1) **Parent Application Access Token (For Partners Only)**: You can get this by running the "Parent Application Access Token" API present under:

     "Recruiter System Connect" -> "Module 1 - Configure Customer Middleware Integrations (Partner Only)" -> "Provision Customer (Child) Applications". 
     
     Your Postman collection will automatically save the value of this access token in its environment & use it for every API you execute under the "Provision Customer (Child) Applications" section. Thus, you do not have to worry about setting the Authorization header every time.

2) **Child Application Access Token**: You can get this by running the "Get Customer Application Access Token" API present under the :

    "Recruiter System Connect" parent folder. 

    Your Postman collection will automatically save the value of this access token in its environment & use it for every API you execute other than the ones under the "Provision Customer (Child) Applications" section.

## Additional Information

### Attach Person URN to Candidate

As per Sync Candidates Documentation, there is a section on "Attach Person URN to Candidate". In Postman Collection, you can find the API named "One Click Export - Attach Person URN" under: 

"Recruiter System Connect" -> "Module 2 - Sync data from ATS to Linkedin" -> "Sync Candidates" section. 

To be able to manually attach a candidate in your ATS with their Linkedin Profile, you need to know their "Person URN" first. There are multiple ways ATS can find out the Person URN: 
1) Via One Click Export 
2) Via Profile Plugin Linking feature 
3) Manually get Person ID via 3 legged OAuth Flow. Refer to 'How to get Person ID for Sync ACL Assignees' section below

> [!IMPORTANT] Please note that as long as you are making sure to link the candidate via steps 1 & 2, you should be good. Step 3 is mostly for manual validation purposes (without using Profile Plugin) and need not be implemented explicitly via ATS.

### Updating JavaScript Domains for Customer/Child Applications

For your "ats-integration-configuration-plugin" & "profile-plugin" widgets to work in your local, development or production environments, you have to first make sure that the domains the widget is hosted on is whitelisted. You can do this by updating your child/customer application by providing the domain URL (without the last '/') for the "validJsSdkDomains" field. Refer to below API in Postman Collection:

"Recruiter System Connect" -> "Module 1 - Configure Customer Middleware Integrations (Partner Only )" -> "Update JavaScript SDK Domain for Child Application"

### How to get Person ID for Sync ACL Assignees

This requires 3 legged OAuth Flow. For your Child application to do 3 legged 
OauthFlow: 

- First configure the OAuth redirection URL by updating the 'oauth2AuthorizedCallbackUrls' field. Refer to below API in Postman Collection:

    "Provision Child Application" API under "Recruiter System Connect" -> "Module 1 - Configure Customer Middleware Integrations (Partner Only )" -> "Update OAuth2.0 Authorized CallBack URL for Child Application".

- Execute the below API in Postman Collection:

    "Recruiter System Connect" -> GET Person ID - With 3 legged OAuth Flow - r_liteprofile permission

    This helps you perform the 3 legged OauthFlow. You will get the Person ID value in response and it will also be automatically set in the 'person_id' environment variable. The same variable is referred in 'Upsert Entity ACL Assignees' so that you don't have to set it explicitly. Simply execute the API after executing the 'GET Person ID' API. Note: This assumes that your application has r_liteprofile permission granted.

### Module 5 - Delete Synced Data APIs

The Delete APIs provided in Module 5 section should not only be used for syncing deletion of individual artifacts like candidates, notes e.t.c. but also used when serving bulk cleanup or contract data deletion requests. 

Note: Delete Application API will also delete Notes, Interview Feedback and Interview Stages associated with it.

