# CHS Payroll: *Tax Email Script* <sup><sup>Task 22516988</sup></sup>
## ZOHO Desk
- New **Workflow** `Complete Tax Ticket` for **Tickets**
    - Completes the ticket information when a ticket was created from a specific email source.
    - Triggers on **Create**
    - For any Tickets
        - **Actions** 
            - Calls the function [Update Tax Ticket](#updateTaxTicket)

- New **Function** `Update Tax Ticket` <a name="updateTaxTicket" />
    - Completes the ticket information when a ticket was created from a specific email source.
    - Here's a detail about the execution.
    - [void updateTaxTicket (int ticket_id)](updateTaxTicket.dg)
    - Input:
        - _(Int)_ ticket_id: The Ticket ID.

- New **Connection** `Desk OAuth` for service **Zoho OAuth**
    - Link name: **deskoauth**
    - Scopes
        - Desk.tickets.READ
        - Desk.tickets.WRITE
        - Desk.tickets.UPDATE

# Video:
<p align="center">
    <a href="https://drive.google.com/open?id=1zhc8UfpQQOEn8jJDvFMLaYx-hxK_d_Hh">
        <img src="https://i.imgur.com/Yc9K1Zf.png" width="720" height="405">
    </a>
</p>