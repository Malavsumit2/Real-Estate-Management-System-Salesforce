# 🏠 Real Estate Management System with Agentforce (Salesforce)

A Salesforce CRM-based Real Estate Management System designed to manage property listings, units, opportunities, and site visits. The application combines Salesforce automation with an **AI-powered Agentforce Real Estate Assistant** that helps customers search properties, schedule visits, retrieve visit details, and manage property opportunities through natural-language conversations.

**Duration:** Aug 2026 – Oct 2026

## 🛠 Tech Stack

- Salesforce CRM
- Salesforce Agentforce
- Apex
- SOQL
- Lightning Web Components (LWC)
- Salesforce Flows (Screen Flows & Autolaunched Flows)
- Record-Triggered Flows
- Validation Rules
- Permission Sets and Profiles
- Agentforce Subagents and Agent Actions

## ✨ Core Salesforce Features

- **Property & Project Management** – Manage real estate projects and their associated units with details such as location, property type, pricing, availability, and status.
- **Unit Management** – Track available, sold, and on-hold units.
- **Site Visit Management** – Create and manage customer property visits linked to projects and units.
- **Automated Visit Scheduling** – Screen Flows guide users through the property visit booking process.
- **Status-Based Automation** – Automatically update related records based on changes in property and visit statuses.
- **Opportunity Management** – Track customer opportunities, selling amounts, received payments, and outstanding balances.
- **Data Integrity** – Validation Rules and Flow-based validations prevent invalid records and inconsistent transactions.
- **Secure Access** – Implement role-based access using Profiles, Permission Sets, OWD, Role Hierarchy, and Sharing Rules.

## 🤖 Agentforce – AI-Powered Real Estate Assistant

Developed an intelligent Real Estate Assistant using Salesforce Agentforce to handle customer queries and automate property-related operations through natural-language conversations.

The agent understands customer requests, routes them to the appropriate subagent, executes Salesforce actions, and responds using real-time CRM data.

### Agent Architecture

The solution follows a modular, subagent-based architecture:

**Customer → Agent Router → Specialized Subagent → Agent Action → Salesforce Flow / Apex → Salesforce Records → Customer Response**

### Subagents Implemented

| Subagent | Responsibility |
|---|---|
| Agent Router | Understands customer intent and routes requests to the appropriate subagent. |
| Property Search | Searches available properties based on location, budget, unit type, and bedroom requirements. |
| Property Visit Booking | Handles customer property visit scheduling and booking validations. |
| Property Visit Details | Retrieves existing visit details using customer and property information. |
| Opportunity Management | Handles opportunity creation, payment updates, and property availability checks. |
| Escalation | Handles requests that require human assistance and escalation. |
| Ambiguous Question | Handles unclear or incomplete customer queries. |
| Off Topic | Handles queries unrelated to real estate operations. |

### Agent Actions Developed

#### 1. Search Available Properties
- Searches available units using customer-provided filters.
- Supports location-based property searches.
- Filters properties based on maximum budget.
- Supports unit type and bedroom-based filtering.
- Retrieves matching property and unit information from Salesforce records.
- Considers project status and unit availability.

#### 2. Book Property Visit
- Books property visits for existing and new customers.
- Captures customer name, project, unit, visit date/time, and remarks.
- Validates customer and project information.
- Verifies that the selected unit belongs to the selected project.
- Checks unit availability before booking.
- Prevents booking for sold or on-hold units.
- Uses confirmation before creating a visit.

#### 3. View Property Visit Details
- Retrieves existing property visit records.
- Searches visits using customer, project, and unit information.
- Displays visit number, customer, project, unit, visit date/time, status, and remarks.
- Supports retrieving multiple matching visits.

#### 4. Create Opportunity
- Creates property-related opportunities for customers.
- Associates opportunities with the selected project and unit.
- Validates customer, project, and unit details.
- Verifies unit availability before opportunity creation.
- Validates the selling amount against the actual unit price.
- Initializes the received payment amount to zero.
- Updates the unit status to Hold after successful opportunity creation.
- Uses customer confirmation before creating an opportunity.

#### 5. Update Opportunity
- Updates the amount received against an existing opportunity.
- Retrieves the correct customer, project, unit, and opportunity.
- Validates payment amounts before updating records.
- Prevents negative payments and overpayments.
- Handles partial and full payment scenarios.
- Automatically updates the unit status to Sold when full payment is received.
- Updates the opportunity stage to Closed Won after full payment.
- Prevents further updates to already-sold properties.

### Agentforce Validations & Business Rules

Implemented business-level validations to maintain data accuracy and prevent invalid operations:

- Only available units can be booked for property visits.
- A unit must belong to the selected project.
- Full customer names are required for property visit booking.
- Invalid project and unit combinations are rejected.
- Opportunity selling amounts must match the listed unit price.
- Negative payment amounts and payments exceeding the selling amount are rejected.
- Full payment automatically marks the unit as Sold.
- Already-sold properties cannot be updated through the opportunity payment process.
- Customer confirmation is required for important booking and opportunity operations.

### Human Handoff & Conversation Handling

- Configured an escalation subagent for requests requiring human assistance.
- Implemented routing for ambiguous and unrelated customer queries.
- Used specialized subagents to keep different real estate operations modular and maintainable.
- Configured Agent Actions to interact with Salesforce records through Flows and Apex.

## 🗂 Data Model

The application uses custom Salesforce objects and standard CRM objects to manage real estate operations.

| Object | Purpose |
|---|---|
| Project__c | Stores real estate project details such as location, project type, status, starting price, and description. |
| Unit__c | Stores individual property unit details, including unit number, type, price, area, floor, bedrooms, and availability status. |
| Visit__c | Stores customer property visit details, including project, unit, visit date/time, status, and remarks. |
| Opportunity | Tracks customer deals, selling amount, received payments, and outstanding balances. |
| Account | Stores customer information. |

### Important Relationships & Fields

- Project__c → Unit__c: Parent-child relationship.
- Opportunity → Project__c: Lookup relationship.
- Opportunity → Unit__c: Lookup relationship.
- Visit__c → Project__c: Lookup relationship.
- Visit__c → Unit__c: Lookup relationship.
- Visit__c → Account: Customer relationship.

**Important Opportunity Fields:**
- Selling_Amount__c
- Amount_Received__c
- Amount_Due__c (Formula Currency)
- Projects__c
- Unit__c
- Last_Follow_up_Date__c

## ⚙️ Automation

### Screen Flows
- Property Visit Booking Flow – Guides users through the visit scheduling process.

### Autolaunched Flows
- Search Available Properties
- Book Property Visit
- View Property Visit Details
- Create Opportunity
- Update Opportunity
- Validate Opportunity Amount

### Record-Triggered Flows
- Automate record updates based on changes in record status and business conditions.

### Apex Integration
- Used Apex and SOQL where required to support Salesforce automation and Agentforce operations.

## 🔐 Security Model

| Layer | Purpose |
|---|---|
| Profiles | Defines baseline object and application permissions. |
| Permission Sets | Grants additional access to required objects and functionality. |
| Field-Level Security | Controls field visibility and edit access. |
| OWD | Defines baseline record-level access. |
| Role Hierarchy | Provides managerial access to subordinate records. |
| Sharing Rules | Extends record access based on business requirements. |
| Agent Permissions | Configures object and field access for the Agentforce execution user. |
| Validation Rules | Enforces data quality and business constraints. |

## 🔮 Future Enhancements

- Lightning dashboards and reports for property listings, visits, and opportunities.
- Email notifications and reminders for scheduled property visits.
- Lightning Web Component for an advanced property search interface.
- Enhanced conversational property recommendations.
- Integration with external real estate listing platforms.
- Enhanced Agentforce voice-based property assistance.

## 👤 Author

**Sumit Malav** – [LinkedIn](https://linkedin.com/in/sumit-malav-2a143b24a) | [GitHub](https://github.com/Malavsumit2)
