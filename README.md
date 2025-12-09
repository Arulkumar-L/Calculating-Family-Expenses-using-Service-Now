# Family Expenses Management System – ServiceNow

A complete ServiceNow implementation created as part of the **SmartBridge Virtual Internship**, featuring custom tables, forms, business rules, and automated record handling.


# Project Overview

The **Family Expenses Management System** helps manage monthly household expenses by categorizing entries, tracking spending, generating insights, and automating common tasks through ServiceNow configuration and scripting.

This project demonstrates:

* Table creation
* Form & field design
* Business Rule automation
* GlideRecord usage
* Relationships
* UI enhancements
* Reporting
* Real-time record updates


## 📌 Objectives

* Create a custom application on ServiceNow
* Build a structured table for storing expense details
* Automate updates using a Business Rule
* Maintain data consistency using relationships
* Display expenses with readable forms and lists
* Generate outputs and screenshots for evaluation


## 🧱 System Architecture

### ✔ Custom Table

**Table Name:** `u_family_expenses`
**Purpose:** Store expense details for all family members.

### Fields Created

| Field Label | Field Name    | Type        | Description                              |
| ----------- | ------------- | ----------- | ---------------------------------------- |
| Expense ID  | u_expense_id  | Auto Number | Unique identifier                        |
| Name        | u_name        | String      | Person who spent                         |
| Category    | u_category    | Choice      | (Food, Travel, Shopping, Medical, Other) |
| Amount      | u_amount      | Currency    | Spending amount                          |
| Date        | u_date        | Date        | Expense date                             |
| Description | u_description | String      | Short description                        |
| Month       | u_month       | Choice      | Used for monthly tracking                |


## 📝 Form Design

The form includes:

* Well-grouped fields
* Category-based filtering
* Mandatory fields for consistent data
* Clear labels and layout


## ⚙️ Business Rule (Auto-fill Fields Based on Category)

### **Rule Name:** Auto Populate Expense Details

### **When:** Before Insert

### **Purpose:** Automatically fill description & categorize records

### **Formatted Script**

```javascript
(function executeRule(current, previous /*null when async*/) {

    var FamilyExpenses = new GlideRecord('u_family_expenses');
    FamilyExpenses.addQuery('u_date', current.u_date);
    FamilyExpenses.query();

    var line = "\n>" + current.u_comments + ": Rs." + current.u_expense + "/-";

    if (FamilyExpenses.next()) {
        FamilyExpenses.u_amount += current.u_expense;
        FamilyExpenses.u_expense_details += line;
        FamilyExpenses.update();
    } else {
        var NewFamilyExpenses = new GlideRecord('u_family_expenses');
        NewFamilyExpenses.u_date = current.u_date;
        NewFamilyExpenses.u_amount = current.u_expense;
        NewFamilyExpenses.u_expense_details = line;  // initialize instead of +=
        NewFamilyExpenses.insert();
    }

})(current, previous);

```
## 🔗 Table Relationship

* **Family Member Table (Parent)** → **Expenses Table (Child)**
* Relationship ensures correct mapping and restricts orphan expenses.

---

## 🖥️ Outputs

* Successful creation of expense records
* Auto-filled descriptions for specific categories
* Clean list view
* Sorted monthly expenses
* Working business rule

---

## 📸 Screenshots Included

All screenshots are available inside the `/screenshots` folder:

* Table Schema
* Form Layout
* Record Insert
* Business Rule
* Output results
* List view
* Demo images

---

## 📂 Repository Structure

```
📁 family-expenses-servicenow
│── README.md
│── documentation/
│     └── Family_Expenses_Project_Report.pdf
│── scripts/
│     └── business_rule.js
│── screenshots/
│     └── (all project screenshots)

```


## ▶️ Demo Video

` https://drive.google.com/file/d/1NNmvheWOF3EF1BjBVhZyag_qAfFfZvt4/view?usp=drive_link `


## 🏁 Conclusion

This project demonstrates core ServiceNow development abilities such as:

* Table & form creation
* Scripting with Business Rules
* UI policy & ACL fundamentals
* Relational data modeling
* Automation & workflow understanding


## 🔮 Future Enhancements

✔ Add analytics dashboard
✔ Add role-based access (Admin/Viewer)
✔ Add monthly expense report PDF export
✔ Create a Flow Designer automation
✔ Add mobile view optimization


