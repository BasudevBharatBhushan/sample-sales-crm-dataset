# 🧠 CRM + Sales Relational Dataset

This dataset simulates a realistic CRM (Customer Relationship Management) and Sales system, ideal for testing multi-table reporting, ETL pipelines, and relational databases.
🧬 This dataset was synthetically generated using ChatGPT.

---

## 📦 Tables Included

### 1. `Contacts.csv`
Contains basic information about individuals or organizations.

| Field         | Description               |
|---------------|---------------------------|
| `ContactID`   | Unique identifier         |
| `FullName`    | Full name                 |
| `Email`       | Email address             |
| `Phone`       | Phone number              |
| `City`        | City (US-based)           |
| `State`       | State (US-based)          |
| `Country`     | Country (`USA`)           |

---

### 2. `Products.csv`
Defines the product catalog.

| Field         | Description                   |
|---------------|-------------------------------|
| `ItemNo`      | Product ID                    |
| `ItemName`    | Product name                  |
| `UnitPrice`   | Unit price                    |
| `Inventory`   | Stock available               |
| `Category`    | Product category              |
| `IsActive`    | Whether product is active     |

---

### 3. `Sales.csv`
Represents actual sales made to contacts.

| Field         | Description               |
|---------------|---------------------------|
| `SalesID`     | Unique sale ID            |
| `ContactID`   | FK → `Contacts.ContactID` |
| `SalesDate`   | Date of transaction       |
| `PaymentStatus` | Paid, Pending, Overdue  |

---

### 4. `SalesLines.csv`
Line-item level data linked to each sale.

| Field         | Description                         |
|---------------|-------------------------------------|
| `LineID`      | Unique line item ID                 |
| `SalesID`     | FK → `Sales.SalesID`                |
| `ItemNo`      | FK → `Products.ItemNo`              |
| `Quantity`    | Units sold                          |
| `LinePrice`   | Calculated: Quantity × Unit Price   |
| `ProfitMargin`| Margin %                            |
| `Tax`         | Tax %                               |

---

### 5. `Leads.csv`
Represents potential customers or business opportunities.

| Field         | Description                         |
|---------------|-------------------------------------|
| `LeadID`      | Unique lead ID                      |
| `ContactID`   | FK → `Contacts.ContactID`           |
| `LeadSource`  | Source (e.g., Website, Referral)    |
| `LeadStatus`  | Status (e.g., New, Qualified)       |
| `CreatedDate` | Date created                        |
| `Notes`       | Additional info                     |

---

### 6. `Activity.csv`
Represents CRM activities associated with leads.

| Field         | Description                         |
|---------------|-------------------------------------|
| `ActivityID`  | Unique activity ID                  |
| `LeadID`      | FK → `Leads.LeadID`                 |
| `ActivityType`| e.g., Call, Email, Meeting          |
| `Subject`     | Activity subject line               |
| `DueDate`     | When it's due                       |
| `Completed`   | Boolean                             |
| `Notes`       | Optional notes                      |

---

### 7. `Opportunity.csv`
Represents potential deals associated with an activity.

| Field            | Description                        |
|------------------|------------------------------------|
| `OpportunityID`  | Unique opportunity ID              |
| `ActivityID`      | FK → `Activity.ActivityID`         |
| `OpportunityStage` | Stage (Prospecting, Negotiation, etc.) |
| `EstimatedValue` | Expected deal value ($)            |
| `CloseDate`      | Anticipated close date             |
| `SalesID`        | (optional) FK → `Sales.SalesID`    |

---

## 🔗 Relationships Overview


```mermaid
erDiagram
    CONTACTS ||--o{ SALES : has
    CONTACTS ||--o{ LEADS : has
    SALES ||--o{ SALESLINES : contains
    SALESLINES }o--|| PRODUCTS : references
    LEADS ||--o{ ACTIVITY : creates
    ACTIVITY ||--|| OPPORTUNITY : drives
    OPPORTUNITY }o--|| SALES : converts




