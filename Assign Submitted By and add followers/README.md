<sup><sup><p align="right">**Task 22544244**</p></sup></sup>
# CHS Payroll: *Assign "Submitted By" and add followers*
## ZOHO Flow
- New **Flow** `Ticket Creation Form`
    - Changes the field "Ticket Creator" to an agent's name with a corresponding email and adds two followers to the ticket.
    - Add app trigger from **ZOHO Forms**
        - Select: **Entry submitted - New version**
        - If there's no connection to **ZOHO Forms**, create one
            - Click on `NEW`
            - Find **ZOHO Forms**
            - Name the connection
            - On *Use this connection to execute*
                - Select **Only specific triggers and actions**
                - Checkmark only **Entry Submitted - New Version**
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
                - Click the agent to add as a follower
                - Copy the last number from the URL
                    - i.e. `https://desk.zoho.com/support/ORG_NAME/ShowHomePage.do#setup/users-control/agents/615417000000168353`
                - Paste **615417000000168353** in value
            - Click `Done`
        - Rename this step to **Follower 1 ID**
    - In Flow > Logic > Flow Control
        - Add a `Select Variable` step after the previous one
            - Rename Variable if needed, in our case is *follower_2_id*
             - **Value**
                - Go to ZOHO Desk > Settings > Users And Control > Agents
                - Click the agent to add as a follower
                - Copy the last number from the URL
                    - i.e. `https://desk.zoho.com/support/ORG_NAME/ShowHomePage.do#setup/users-control/agents/615417000000139001`
                - Paste **615417000000139001** in value
            - Click `Done`
        - Rename this step to **Follower 2 ID**
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
        - If there's no connection to **ZOHO Desk**, create one
            - Click on `MY CONNECTIONS`
            - Click on `CREATE CONNECTION`
            - Fin **ZOHO Desk**
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

# Video:
<p align="center">
    <a href="https://drive.google.com/open?id=1heTJmHOyHcTsk4C3EAb3BuwOqzRE2hAs">
        <img src="https://i.imgur.com/Yc9K1Zf.png" width="720" height="405">
    </a>
</p>    