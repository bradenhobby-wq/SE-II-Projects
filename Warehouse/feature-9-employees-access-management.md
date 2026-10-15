# Feature: Employees Access Management
**Feature ID:** 9
**Branch pattern:** `feature/employees-access-management`
**Status:** Draft
**Created:** 2026-10-11
**Input:** Maintain employees - add, edit and delete.
**Depends on:** [Feature X — …](feature-X-….md)

## User Stories
### US-9.1: Add Employees
**As a** manager
**I want to** be able to add employees
**So that** the employees list can be updated

**Priority:** P1
**Independent test:** The manager adds a new employee with a valid password
**Acceptance scenarios:** see ### US-9.1 under Acceptance
Criteria

### US-9.2: Update Employees
**As a** employee
**I want to** update my own information
**So that** the database is up to date

**Priority:** P1
**Independent test:** An existing employee updates their own information
**Acceptance scenarios:** see ### US-9.2 under Acceptance
Criteria

### US-9.3: Delete Employees
**As a** manager
**I want to** delete employees from the database
**So that** old employees do not have access anymore

**Priority:** P1
**Independent test:** Create an employee account, delete said account
**Acceptance scenarios:** see ### US-9.3 under Acceptance
Criteria

### US-9.4: Search Employees
**As a** manager
**I want to** search the employees
**So that** I can easily access their information

**Priority:** P2
**Independent test:** Create 20+ employees, search them by name/id
**Acceptance scenarios:** see ### US-9.4 under Acceptance
Criteria

## Requirements
### Functional Requirements
- **FR-001**: Managers can search employees by name or id
- **FR-002**: Employees CANNOT update their role or employee id
- **FR-003**: The four roles are: 1. "Inventory Clerk" 2. "Warehouse Worker" 3. "Shipping Clerk" 4. "Driver" 5. "Warehouse Manager" 6. "Company Manager"
- **FR-004**: The manager enters in the information for the employees. All fields except for employee id and password are required
- **FR-005**: If the employee changes their password when editing their information, they must provide a verification code from their email

## Key Entities
- **Employee**: A worker for the warehouse who is allowed to perform certain tasks on the app
## Data Model Requirements
### `Employee` table
| Field | Type | Rules |
|-------|------|-------|
| `employeeId` | INTEGER PK | Auto-increment |
| `name` | STRING(100) | Required |
| `password` | STRING(255) | Bcrypt hash only |
| `role` | STRING(20) | Required; Only six roles in existence |
| `email` | STRING(40) | Required |


## Acceptance Criteria

### US-9.1 — Add Employees
#### Scenario: Employee Successfully Added
* **Given** a manager has logged in and navigated to the employees page
* **When** they submit the form to add an employee
* **And** they DID specify the name, email, or role of an employee
* **Then** an employee account is created
* **And** the system responds "[Employee Name] successfully added"
#### Scenario: Not All Required Fields Filled Out
* **Given** a manager has logged in and navigated to the employees page
* **When** they submit the form to add an employee
* **And** they DID NOT specify either the name, email, or role of an employee
* **Then** an employee account is NOT created
* **And** the system responds "Complete the following fields: [empty fields]"
#### Scenario: Cancel Button Clicked
* **Given** a manager has logged in and navigated to the employees page
* **When** they are filling out the form to add an employee
* **And** they click the cancel button
* **Then** an employee account is NOT created
* **And** the UI returns to the previous screen

### US-9.2 — Update Employees
#### Scenario: Information Successfully Updated
* **Given** a manager has logged in and navigated to the employees page
* **When** they submit the form to edit an employee's information
* **Then** the employee account is updated
* **And** the system responds "[Employee Name] successfully updated"
#### Scenario: Verification Code Entered To Change Password
* **Given** an employee exists and changed their password
* **When** they enter the right verification code
* **And** they provide a strong password
* **Then** the API returns '200' and the password is saved
* **And** the system responds "Password successfully saved"
#### Scenario: Invalid Verification Code
* **Given** an employee exists
* **And** the employee has requested a verification code to change their password
* **When** they provide the incorrect verification code
* **Then** the API returns '400'
* **And** the system responds "Invalid verification code"
#### Scenario: Weak Password Rejected
* **Given** an employee exists and has requested to change their password
* **And** they have verified their email
* **When** they do NOT provide a strong password
* **Then** they are NOT logged in and the API returns '400'
* **And** the system responds "Password must be 12+ characters long and have one uppercase letter, lowercase letter, symbol, and number."
#### Scenario: Cancel Button Clicked
* **Given** a manager has logged in and navigated to the employees page
* **When** they are filling out the form to edit an employee
* **And** they click the cancel button
* **Then** the employee account is NOT updated
* **And** the UI returns to the previous screen

### US-9.3 — Delete Employees
#### Scenario: Employee Sucessfully Deleted
* **Given** a manager has logged in and navigated to the employees page
* **When** they confirm that they want to delete an employee
* **Then** that employee is deleted from the database
* **And** the System responds "[Employee Name] successfully deleted"

### US-9.4 — Search Employees
#### Scenario: Matching Search Results Appear For Name
* **Given** a manager has logged in and navigated to the employees page 
* **When** the manager searches for a employees by name
* **Then** employees with similar names appear at the top of the search results
#### Scenario: Matching Search Results Appear For Name
* **Given** a manager has logged in and navigated to the employees page 
* **When** the manager searches for an employee by id
* **Then** the employee with that exact id is the only search result
#### Scenario: No Employees With That ID
* **Given** a manager has logged in and navigated to the employees page 
* **When** the manager searches for a employee by name
* **And** no employee has that id
* **Then** no employees appear in the search results
* **And** the system returns a "No Matching Employee" error to the user 
