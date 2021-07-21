<sup><sup><p align="right">**Task 22599726**</p></sup></sup>
# CHS Payroll: *Attach Form Registry as CVS*
## ZOHO Flow
- New **Flow** 
    - Flow name: `Ticket Creation Form Webhook`
    - Flow Description: *Copies the registry information of a form to a CVS file and attach it to the Desk ticket.*
    - Add a **Webhook** trigger
        - Select **JSON** as **Payload Format** 
        - Select: **Entry submitted - New version**
        - Copy the Webhook **URL**
        - Click `Next`
        - Click `Test`
        - Go an configure the [Webhook Integration](#WebhookFlow) in flow
        - Click `Done`
    - In Flow > Logic > Custom Functions
        - Click on `+ Custom Function`
        - Function name **uploadFormRegistryTicket**
        - Return type **string**
        - Input Parameters
            | Name  | Type  |
            | :---: | :---: |
            **entry_form** | `map`
        - Copy the content of ***updateTicketForm.dg***
        - If there's no connection to **ZOHO Desk**, create one
            - Click on `MY CONNECTIONS`
            - Click on `CREATE CONNECTION`
            - Find **ZOHO Desk**
            - Name the connection
            - On *Use this connection to execute*
                - Select **Only specific triggers and actions**
                - Checkmark
                    - **Triggers > Ticket Created**
                    - **Actions > Fetch Ticket**
                    - **Actions > Update Ticket**
                    - **Actions > Fetch Agent**
                - Click `Authorize`
                - Click `Accept`
            - You can find this connection name by clicking on `VIEW DETAILS`
        - Update the information required in the function
            - Line 19, update **org_id**
            - Line 21, update **ticket_creator_api_name**
            - Line 33, update *connection* to the ZOHO Desk connection name
            - Line 48, update the last argument of zoho.desk.searchRecords to the ZOHO Desk connection name
            - Line 63, update the last argument of zoho.desk.update to the ZOHO Desk connection name
            - Line 83, update *connection* to the ZOHO Desk connection name
        - Click `Save`
        - Click the [X] mark in the top right corner
        - Add `updateTicketForm` as the last step to the flow
            - follower_1_id
                - Click **Follower 1 ID** in the list to the right
                - Select your variable 
            - follower_2_id
                - Click **Follower 2 ID** in the list to the right
                - Select your variable 
            - email
                - Click **Entry submitted - New version** in the list to the right
                - Select **Submitted By**
            - ticket_subject 
                - Click **Entry submitted - New version** in the list to the right
                - Select **Subject**
    - In the upper right corner, click on `YOUR FLOW IS` from **OFF** to **ON**
    - Test the Flow creating an entry in your form.

## ZOHO Forms
- Webhook Integration <a name="WebhookFlow" />
    - Go to ZOHO Forms > My Forms > In the form you want to add this click `Edit`
    - Go to Integrations > Find **Webhook** in the list to the left
    - Click `Configure Webhook`
    - Webhook URL: Paste the **FLow Webhook URL**
    - Content Type: **application/json**
    - Payload parameters
        - For each field in the pick list, select the field.
        - In *Parameter Name* copy the name and change the spaces to "\_"
    - Click `Test Webhook`
    - Click `Run Test`
    - If a success message appears, click `Ok` then click `Save`

# Video:
<p align="center">
    <a href="https://drive.google.com/open?id=1heTJmHOyHcTsk4C3EAb3BuwOqzRE2hAs">
        <img src="https://i.imgur.com/Yc9K1Zf.png" width="720" height="405">
    </a>
</p>    