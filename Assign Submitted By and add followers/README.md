# CHS Payroll: *Assign "Submitted By" and add followers.* <sup><sup>Task 22544244</sup></sup>
## ZOHO Flow
- New **Flow** `Ticket Creation Form`
    - Changes the field "Ticket Creator" to a agent's name with a corresponding email and adds two followers to the ticket.
    - Add app trigger from **Zoho Forms**
        - Select: **Entry submitted - New version**
        - If there's not connection to flow, create one
            - Click on `NEW`
            - Name the connection
            - On *Use this connection to execute*
                - Select **Only specific triggers and actions**
                - Check mark only **Entry Submitted - New Version**
                - Click `Authorize`
                - Click `Accept`
        - Select the form from the pickup list.
        - Leave the **Filter Criteria** empty.
        - Click `Done`
    - From Logic > Flow Control
        - Add a `Delay` step after the trigger
        - In **Delay for** type: '1 minute' (without the apostrophes)
        - Click `DONE`
    - From Logic > Flow Control
        - Add a `Select Variable` step after the previous one
            - Rename Variable if needed, in our case is *follower_1_id*
             - **Value**
                - Go to ZOHO Desk > Settings > Users And Control > Agents
                - Click the agent to add as follower
                - Copy the last number from the url
                    - https://desk.zoho.com/support/ORG_NAME/ShowHomePage.do#setup/users-control/agents/615417000000168353
                - Paste **615417000000168353** in value
            - Click `Done`
        - Rename this step to **Follower 1 ID**
    - In Flow > Logic > Flow Control
        - Add a `Select Variable` step after the previous one
            - Rename Variable if needed, in our case is *follower_2_id*
             - **Value**
                - Go to ZOHO Desk > Settings > Users And Control > Agents
                - Click the agent to add as follower
                - Copy the last number from the url
                    - https://desk.zoho.com/support/ORG_NAME/ShowHomePage.do#setup/users-control/agents/615417000000139001
                - Paste **615417000000139001** in value
            - Click `Done`
    - In Flow > Logic > Custom Functions
        - Click on `+ Custom Function`
        - Function name **updateTicketForm**
        - Return type **string**
        - Input Parameters
            | Name  | Type  |
            | :---: | :---: |
            **follower_1_id** | `int`
            **follower_2_id** | `int`
            **email** | `string`
            **ticket_subject** | `string`
        - Copy the content of ***updateTicketForm.dg***
        - If there's not connection to **ZOHO Desk**, create one
            - Click on `MY CONNECTIONS`
            - Name the connection
            - On *Use this connection to execute*
                - Select **Only specific triggers and actions**
                - Check mark
                    - **Triggers > Ticket Created**
                    - **Actions > Fetch Ticket**
                    - **Actions > Update Ticket**
                    - **Actions > Fetch Agent**
                - Click `Authorize`
                - Click `Accept`
            - You can find this connection name clicking on `VIEW DETAILS`
        - Update the information required in the function
            - Line 19, update **org_id**
            - Line 21, update **ticket_creator_api_name**
            - Line 33, update connection to the ZOHO Desk connection name
            - Line 48, update the last argument of zoho.desk.searchRecords to the ZOHO Desk connection name
            - Line 63, update the last argument of zoho.desk.update to the ZOHO Desk connection name
            - Line 83, update connection to the ZOHO Desk connection name
        - Click `Save`
        - Click the [X] mark in the top right corner
        - Add `updateTicketForm` as the last step to the flow
            - ticket_id
                - Click **Ticket created** form the list to the right
                - Select **Ticket ID**
            - follower_1_id
                - Click **Follower 1 ID** form the list to the right
                - Select your variable 
            - follower_2_id
                - Click **Follower 2 ID** form the list to the right
                - Select your variable 
    - In the upper right corner, click on `YOUR FLOW IS` from **OFF** to **ON**
    - Test the Flow creating an entry in your form.

# Video:
<p align="center">
    <a href="DriveURL">
        <img src="https://i.imgur.com/Yc9K1Zf.png" width="720" height="405">
    </a>
</p>