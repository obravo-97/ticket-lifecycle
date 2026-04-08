<p align="center">
  <img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

# osTicket: Ticket Lifecycle Examples

This repository documents **end-to-end ticket lifecycle workflows** in osTicket, from ticket creation by end users to triage, escalation, assignment, and resolution by help desk staff.

This is Part 3 of a three-part osTicket project series:

- [osTicket: Prerequisites and Installation (Part 1)](https://github.com/kylekincaid/osticket-prereqs)
- [osTicket: Post-Installation Configuration (Part 2)](https://github.com/kylekincaid/post-install-config)
- osTicket: Ticket Lifecycle Examples (Part 3) 
---

## Access URLs

Use the following URLs throughout this exercise:

- Admin / Analyst (Staff Control Panel):
  http://localhost/osTicket/scp/login.php

- End User Portal:  
  http://localhost/osTicket

---

## Lab Objective

In this section, we will:

- Create tickets as end users
- Observe and manage ticket properties as help desk agents
- Understand how departments, SLAs, priorities, and assignments affect ticket visibility
- Work tickets to completion under different roles
- Observe real-world ticketing behaviors and constraints

This simulation is designed to focus on process and workflow, rather than just clicking buttons.

---

## Initial Configuration/Setup: Create Required Departments (Admin Panel)

The ticket scenarios in this lab assume the following departments exist:

- SysAdmins (used for escalation and access-control behavior)
- Online Banking (used in Ticket Scenario 1)
- Support (used in Ticket Scenarios 2 and 3)
- Maintenance (will be deleted as part of cleanup)

If your osTicket instance does not already have these departments, create them first using the steps below.

---

### 1) Log into the Admin Panel

1. Go to: http://localhost/osTicket/scp/login.php
2. Log in with the admin account John 

<img width="711" height="522" alt="image" src="https://github.com/user-attachments/assets/771f3089-e37b-4218-8b8e-8d8137c6ae12" />

3. In the top navigation, click Admin Panel 

<img width="2084" height="754" alt="image" src="https://github.com/user-attachments/assets/887d744b-3fd2-4623-8047-cd0ed3b2ab74" />


---

### 2) Navigate to Departments

1. In the Admin Panel, click the Agents tab (top navigation)
2. Click Departments
<img width="1192" height="542" alt="image" src="https://github.com/user-attachments/assets/f9afe735-576f-41f5-92af-b8402c75eb69" />

You should now see the Departments list.
<img width="1876" height="838" alt="image" src="https://github.com/user-attachments/assets/64ff4e2e-f4f7-45db-8ddb-4e4e1241af29" />

---

### 3) Create the Required Departments

You will repeat the same process for each department.

#### Click path to add a department
1. On the Departments page, click Add New Department
2. Fill in the Name
3. (If prompted) Choose the department type / settings as defaults unless your lab requires otherwise
4. Click Create Dept (or Add Department, depending on your version)

Create the following departments (one at a time):

- SysAdmins
- Online Banking
- Support


---

### 4) Promote SysAdmins to a Top-Level Department

Now that SysAdmins exists, we will make it a Top-Level Department 

1. In Admin Panel - Agents - Departments
2. Click on SysAdmins (department name) to edit it
3. Locate the Parent Department (or similar) setting
4. Set it to top-Level / No Parent / (wording depends on version)
5. Click Save Changes (or save Dept)


---

### 5) Delete the Maintenance Department 

This lab requires deleting the Maintenance department entirely (not archiving it).

1. In Admin Panel - Agents - Departments
2. Click Maintenance
3. Choose Delete 
4. Confirm the deletion when prompted
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/3e586f9c-0743-49b9-a850-eb2135e5ffcf" />


---

### 6) Confirm Department List Before Proceeding

Before starting Ticket Scenario 1, confirm that the Departments list includes:

- SysAdmins (Top-Level)
- Online Banking
- Support

And that:

- Maintenance is deleted
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/4db1158d-9dcb-49db-9e50-8e30846d37d2" />


---

## Pre-Lab Setup: Agents and Department Access

The ticket lifecycle scenarios in this lab require multiple help desk agents with different department access levels.

During the osTicket installation process (Part 1), an initial administrator account is created. In this lab, that account is named john. Because this account already exists and has administrative access, we will reuse it rather than recreate it.

We will:
- Adjust department access for the existing john account
- Create an additional agent (jane) to demonstrate escalation and role-based access control

---

### Agents Used in This Lab

- john — Initial administrator account  
- jane — Additional agent used for escalation and ticket resolution  

---

## Step-by-Step: Configure Agents in osTicket

### 1) Log into the Admin Panel

1. Navigate to:  
   http://localhost/osTicket/scp/login.php
2. Log in using the john account
3. Click Admin Panel in the top navigation

---

### 2) Navigate to Agents

1. In the Admin Panel, click the Agents tab
2. Click Agents from the sub-menu

You should now see a list of existing agents, for now only john.
<img width="895" height="352" alt="image" src="https://github.com/user-attachments/assets/3e915314-7bf2-4de9-8d38-0ade4f9cf721" />

---

## Configure Existing Agent: john

The john account was created during installation and already has administrative access. In this lab, we will limit department access intentionally to demonstrate escalation behavior later.

### 3) Assign Department Access for john

1. Click john in the Agents list
2. Locate the Department Access section
3. Ensure access is granted to:
   - Support
4. Ensure SysAdmins is not assigned at this stage
5. Save changes

---

## Create New Agent: jane

The jane account will be used to work escalated tickets and demonstrate role-based access control.

### 4) Create Agent jane

1. From the Agents page, click add New Agent
2. Fill in the following fields:

Account Information
- Name: Jane Doe
- Username: jane
- Email: any valid test email
- Password: any password
Access
- Primary Department: SysAdmins
- Role: Agent or Admin

3. Click Create or Add Agent

---

### 5) Assign Department Access for jane

1. Click jane in the Agents list
2. Confirm access to:
   - SysAdmins
   - (Optional) Support
3. Save changes

Jane will be used to resolve escalated tickets that john cannot modify.

---

## Validation Before Proceeding

Before starting Ticket Scenario 1, confirm the following:

- john
  - Can view and work tickets in Support
  - Loses modification access when tickets escalate to SysAdmins

- jane
  - Can access the SysAdmins department
  - Can work escalated tickets to completion
<img width="895" height="438" alt="image" src="https://github.com/user-attachments/assets/9f8d99de-6df8-411f-8f20-b23c46801b4d" />


Once these conditions are met, proceed to the ticket lifecycle scenarios.



---

## Ticket Scenario 1 — Critical Outage (SEV-A)

### End User Action

As an end user, create the following ticket:

Subject: Entire mobile/online banking system is down

Submit the ticket through the End User Portal.

<img width="1050" height="497" alt="image" src="https://github.com/user-attachments/assets/23ae8da9-a734-4fd0-af81-e8fddbe0ab61" />

<img width="1048" height="842" alt="image" src="https://github.com/user-attachments/assets/1f5eb5d6-96ce-41a9-bed6-d0d18c6451a0" />



---

### Help Desk Agent Review (john)

Log in as Help Desk Agent (john) and observe the ticket’s properties:

- Priority
- Department
- SLA
- Assigned To

Do not change anything yet—only observe.

---

### Set Ticket Properties

Update the ticket with the following settings:

- SLA: Sev-A (1 hour, 24/7)
- Department: Online Banking

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/0b971592-7492-4ca3-8522-7cf89211b2a4" />


---

### Access Validation

Attempt to observe the ticket again as john.

- Can you still view the ticket?
- Can you modify the ticket?

Take note of the behavior.

---

### Resolution

Work the ticket to completion as Jane.

---

## Ticket Scenario 2 — Software Request (SEV-B)

### End User Action

As an end user, create the following ticket:

Subject: Accounting department needs Adobe upgrade, broken

<img width="992" height="796" alt="image" src="https://github.com/user-attachments/assets/a87e1a28-c67a-498a-94ce-b3d9840d7864" />

---

### Help Desk Agent Review (john)

Log in as john and observe:

- Priority
- Department
- SLA
- Assigned To

---

### Set Ticket Properties

Update the ticket:

- SLA: Sev-B (4 hours, 24/7)
- Department: Support

<img width="892" height="472" alt="image" src="https://github.com/user-attachments/assets/d353b945-81e0-498f-ac29-74e22c433980" />

---


---

## Ticket Scenario 3 — Executive Hardware Issue (SEV-B)

### End User Action

As an end user, create the following ticket:

Subject: CFO’s laptop will no longer turn on

<img width="895" height="492" alt="image" src="https://github.com/user-attachments/assets/c93e3a51-6da7-469b-b351-315c68911676" />

---

### Help Desk Agent Review (john)

Observe the ticket properties:

- Priority
- Department
- SLA
- Assigned To

---

### Set Ticket Properties

Update the ticket:

- SLA: Sev-B (4 hours, 24/7)
- Department: Support

<img width="1183" height="570" alt="image" src="https://github.com/user-attachments/assets/23d3f8f4-a47a-4f20-b420-c6318f059882" />

---

### Resolution

Work the ticket to completion as john.

---

## Escalation and Permission Behavior

### Escalate All Tickets

Set **all tickets** to:

- SLA: Sev-A  
- Department: SysAdmins (last)

Observe that the tickets become inaccessible to standard agents.

---

### Restore Visibility

1. Switch to the Admin Panel
2. Assign yourself View access to the SysAdmins department
3. Switch back to the Agent Panel

Observe:

- You can now see the escalated ticket
- You can no longer modify it

This demonstrates role-based access control in osTicket.

---

## Final Resolution

Solve all remaining tickets and confirm they are closed properly.
