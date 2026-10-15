# Feature: User Authentication and Verification
**Feature ID:** 11
**Branch pattern:** `feature/user-authentication-and-verification`
**Status:** First Draft
**Created:** 2026-10-12
**Input:** Control access to the POS by account and role; support log in and log out; maintain employee passwords.
**Depends on:** [Feature 9 — Employees Access Management](feature-9-employees-access-management.md)

## User Stories

### US-11.1: Employee Able To Log In
**As a** employee
**I want to** be able to log into the app
**So that** I can do my job

**Priority:** P1
**Independent test:** Have an employee log onto the app
**Acceptance scenarios:** see ### US-11.1 under Acceptance
Criteria

### US-11.2: Employee Can Access Correct Pages
**As a** employee
**I want to** be able to access the page corresponding to my role
**So that** I can use the services I need for my job

**Priority:** P1
**Independent test:** Have every type of employee navigate to their page
**Acceptance scenarios:** see ### US-11.2 under Acceptance
Criteria

### US-11.3: Employee Able To Log Out
**As a** employee
**I want to** be able to log out of the app
**So that** someone can't access my account on the device I was using

**Priority:** P1
**Independent test:** Have an employee log in and log out
**Acceptance scenarios:** see ### US-11.3 under Acceptance
Criteria

### US-11.4: Employee Logged Out After Inactivity
**As a** employee
**I want to** be logged out after I am not active for a while
**So that** I don't accidently leave the account open for malicious users

**Priority:** P2
**Independent test:** An employee logs in, stops being active for the time listed in FR-001, and the system logs the user out after a warning
**Acceptance scenarios:** see ### US-11.4 under Acceptance
Criteria

## Requirements
### Functional Requirements
- **FR-001**: When `currentTime` is four hours [NEED CONFIRMATION ON MAX INACTIVE TIME] greater than `lastLogonTime`, ask the user if they are logged in. If the user does not respond in 10 seconds, delete the `user` object.
- **FR-002**: System MUST create a `user` when an employee successfully logs in
- **FR-003**: System MUST update `currentTime` every second
- **FR-004**: When the user does not have a active app on an active device, `active` becomes false. I.e., when the laptop is closed or the app is clicked off of, `active` becomes false.
- **FR-005**: When `active` is false, set `lastLogonTime` to `currentTime`
- **FR-006**: If no `user` object exists in the current session, the system shows the login screen.
- **FR-007**: The "Manager," "Shipping Clerk," "Inventory Clerk," "Warehouse Worker," and "Driver" pages should be empty. The pages only exist to make sure the verification is functional
- **FR-008**: Pages accessible by a certain role MUST only be viewable by that role. It is not enough for other roles to not be able to go to that page, it should not appear on their side at all
- **FR-009**: The "Manager" page is only accessible by an `Employee` with the `Employee.role` "Manager"
- **FR-010**: The "Shipping Clerk" page is only accessible by an `Employee` with the `Employee.role` "Shipping Clerk"
- **FR-011**: The "Inventory Clerk" page is only accessible by an `Employee` with the `Employee.role` "Inventory Clerk"
- **FR-012**: The "Warehouse Worker" page is only accessible by an `Employee` with the `Employee.role` "Warehouse Worker"
- **FR-013**: The "Driver" page is only accessible by an `Employee` with the `Employee.role` "Driver"
- **FR-014**: The "Company" page is only accessible by an `Employee` with the `Employee.role` "Company Manager"
- **FR-015**: The password MUST have one uppercase letter, one lowercase letter, one special character, one number, and at least twelve total characters. If the password doesn't have this, the system MUST NOT let the employee create their password
- **FR-016**: The employee must enter a verification code from their email to first create their password
- **FR-017**: Company Managers do not have the same access as Warehouse Managers. Company Managers only have access to their Warehouses

## Key Entities
- **User**: A temporary object to keep track of an employee's current session.
## Data Model Requirements
### `User` table
| Field | Type | Rules |
|-------|------|-------|
| `employee` | EMPLOYEE | Required |
| `lastLogonTime` | STRING(200) | Required |
| `currentTime` | STRING(200) | Required |
| `active` | BOOLEAN | Default true |
## Acceptance Criteria

### US-11.1 — Employee Able To Log In
#### Scenario: Password Created On First Log In
* **Given** an employee exists and hasn't created a password
* **When** they first log in
* **Then** they have to go through the "Change Password" process outlined in Feature 9 before they log in
#### Scenario: User Created On First Log In
* **Given** an employee exists
* **When** they log in
* **Then** a new `User` is created with the correct employee
#### Scenario: Log In Successful
* **Given** an employee exists who already created a password
* **When** they log in with the correct password
* **Then** the API returns '200' and the employee see their dashboard
#### Scenario: Invalid Credentials Rejected
* **Given** an employee exists who already created a password
* **When** they log in with the INCORRECT password
* **Then** the API returns '400'
* **And** the system responds "Invalid username or password"

### US-11.2 — Employee Can Access Correct Pages
#### Scenario: Correct Pages Shown
* **Given** an employee exists
* **When** they log into their account
* **Then** the pages they need to access are shown
* **And** pages they are NOT ALLOWED to access are NOT SHOWN
#### Scenario: User Can Navigate to Proper Pages
* **Given** an employee is logged in
* **When** they click on a page in their dashboard
* **Then** the API returns '200' and they can see the page contents


### US-11.3 — Employee Able To Log Out
#### Scenario: User Logs Out
* **Given** an employee is logged in
* **When** they click the button to log out
* **And** they click "Yes" in response to the "Are you sure you want to log out?" pop up
* **Then** they are logged out of their account
* **And** their current `User` object is deleted
#### Scenario: User Cancels Log Out
* **Given** an employee is logged in
* **When** they click the button to log out
* **And** they click "No" in response to the "Are you sure you want to log out?" popup
* **Then** they are NOT logged out of their account

### US-11.4 — Employee Logged Out After Inactivity
#### Scenario: System Asks User If They Are Active
* **Given** an employee is logged in but not active
* **When** they have been inactive for at least four hours
* **Then** the system asks them "Are you still active?"
#### Scenario: System Kicks User Out After Inactivity
* **Given** an employee has logged in and been inactive for four hours
* **And** the system asks if they are active
* **When** they click "Yes" in response to "Are you still active?"
* **Then** they are logged out of their account
* **And** their current `User` object is deleted
#### Scenario: User Is Still Active
* **Given** an employee has logged in and been inactive for four hours
* **And** the system asks if they are active
* **When** they click "Yes" in response to "Are you still active?"
* **Then** they are NOT logged out of their account
