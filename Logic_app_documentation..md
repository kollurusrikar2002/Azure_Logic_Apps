
# Overview of Logic apps in Documentaction 

**The following content is AI generated and might contain incorrect information. Before you use this content, make sure to review for inaccuracies.**    
## Summary    
The purpose of this workflow is to monitor incoming emails in the Inbox folder of the configured Office 365 email account. When a new email arrives, it checks if the email is unread. If it is unread, the email is moved to the "Unreaded_emails" folder. Then, it retrieves the unread emails with attachments from the "Unreaded_emails" folder. For each email, it iterates through the attachments and performs two actions. First, it creates a blob in Azure Blob storage with the attachment content. Then, it analyzes the attachment using Form Recognizer AI service to extract invoice details. Finally, it sends an email to the specified email address with the extracted invoice details.    
||Workflow Properties|Value|    
|-----|-----|-----|    
|1|Connector type - In App|5|    
|2|Connector type - Shared|6|    
|3|Connector type - Custom|0|    
|4|API Connections|5|    
    
# Workflow Steps    
## How the workflow starts (Triggers)    

 - **When_a_new_email_arrives_(V3)**    
&ensp;&ensp; - **Type:** Shared    
&ensp;&ensp; - **Description:** This trigger is activated when a new email arrives in the specified folder in the Office 365 mailbox. It fetches the new email and its attachments.    
&ensp;&ensp; - **Trigger Input:** This trigger requires a connection to the Office 365 mailbox and the following inputs:    
   - `host` - Connection to the Office 365 mailbox  
   - `fetch` - Fetches the new email details including importance, attachments, and folder path  
   - `subscribe` - Sets up a subscription to receive notifications for new emails  
&ensp;&ensp; - **Trigger Output:** This trigger does not have any output as it is the first action in the workflow and does not receive any input from other actions.  
  
## How the workflow continues (Actions)    
 - **Condition**    
&ensp;&ensp; - **Type:** In App    
&ensp;&ensp; - **Description:** This action is used to check if the condition specified is true or false. If the condition is true, the workflow continues with the actions inside the "If true" branch. If the condition is false, the workflow continues with the actions inside the "If false" branch.    
&ensp;&ensp; - **Action Output:** This action does not have any output as it is used for control flow in the workflow and does not generate any data.    
&ensp;&ensp; - Else:    
&ensp;&ensp;&ensp;&ensp; - **Move_email_(V2)**    
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp; - **Type:** Shared    
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp; - **Description:** Moves the email to a specified folder in the Office 365 mailbox.    
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp; - **Action Input:** This action requires a connection to the Office 365 mailbox and the following inputs:    
   - `host` - Connection to the Office 365 mailbox  
   - `method` - Specifies the HTTP method to use for the API request, in this case, "post"  
   - `path` - Specifies the API path to move the email to a different folder  
   - `queries` - Specifies the folder path where the email will be moved to  
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp; - **Action Output:** This action does not have any output as it is used to perform a specific task and does not generate any data.    
&ensp;&ensp;&ensp;&ensp; - **Get_emails_(V3)**    
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp; - **Type:** Shared    
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp; - **Description:** Retrieves the emails that match the specified criteria from the Office 365 mailbox.    
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp; - **Action Input:** This action requires a connection to the Office 365 mailbox and the following inputs:    
   - `host` - Connection to the Office 365 mailbox  
   - `method` - Specifies the HTTP method to use for the API request, in this case, "get"  
   - `path` - Specifies the API path to fetch the emails  
   - `queries` - Specifies the criteria for fetching the emails such as importance, folder path, and filter options  
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp; - **Action Output:** This action does not have any output as it is used to perform a specific task and does not generate any data.    
&ensp;&ensp;&ensp;&ensp; - **For_each_1**    
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp; - **Type:** In App    
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp; - **Description:** This action iterates over the emails fetched in the previous action to perform a specific task for each email.    
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp; - **Action Output:** This action does not have any output as it is used for control flow in the workflow and does not generate any data.    
    &ensp;&ensp;&ensp;&ensp;&ensp;&ensp; - Actions:    
    &ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp; - **For_each**    
    &ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp; - **Type:** In App    
    &ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp; - **Description:** This action iterates over a collection of items to perform a specific task for each item.    
    &ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp; - **Action Output:** This action does not have any output as it is used for control flow in the workflow and does not generate any data.    
    &ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp; - Actions:    
    &ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ens
