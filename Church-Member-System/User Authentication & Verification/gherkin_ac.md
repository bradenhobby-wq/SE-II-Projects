## Acceptance Criteria

### US-4.1 — Staff With Admin Status Add Users
#### Scenario: User Successfully Added
* **Given** I am on the church staff and have admin privileges
* **When** I navigate to the page "Manage Users"
* **And** I type the email to notify
* **Then** that email receives a link to create an account on the website
#### Scenario: User NOT Added
* **Given** I am on the church staff and have admin privileges
* **When** I navigate to the page "Manage Users"
* **And** I type the email to notify
* **Then** that email does not receive a link to create an account on the website


### US-4.2 — Staff With Admin Status Delete Users
#### Scenario: User Successfully Deleted
* **Given** I am on the church staff and have admin privileges
* **When** I navigate to the page "Manage Users"
* **And** I delete a user
* **Then** the System outputs a message like "User successfully deleted"
* **And** the user's login credentials no longer work
#### Scenario: User NOT Deleted
* **Given** I am on the church staff and have admin privileges
* **When** I navigate to the page "Manage Users"
* **And** I delete a user
* **Then** the System does not output a message like "User successfully deleted"
* **Or** the user's login credentials still work


### US-4.3 — Staff With Admin Status Edit Users' Roles
#### Scenario: Role Successfully Changed
* **Given** I am on the church staff and have admin privileges
* **When** I navigate to the page "Edit User's Roles"
* **And** I edit a user's role
* **Then** the System outputs a message like "User's role successfully changed"
* **And** that user has the privileges of the new role
#### Scenario: Role NOT Changed (failure)
* **Given** I am on the church staff and have admin privileges
* **When** I navigate to the page "Edit User's Roles"
* **And** I edit a user's role
* **Then** the System does not output a message like "User's role successfully changed"
* **Or** that user does not have the privileges of the new role


### US-4.4 — Users Use The Forgot Password Option
#### Scenario: Password Successfully Updated
* **Given** I am on the church staff
* **And** I click the "Forgot Password" hyperlink on the login page
* **When** I provide my username and enter a verification code from my email
* **Then** the System does output a message like "Password successfully updated"
* **And** I can log into my account with my new password
#### Scenario: Password NOT Updated
* **Given** I am on the church staff
* **And** I click the "Forgot Password" hyperlink on the login page
* **When** I provide my username and enter a verification code from my email
* **And** I enter a new, strong password
* **Then** the System does not output a message like "Password successfully updated"
* **Or** I cannot log into my account with my new password


### US-4.5 — Users Log In With Correct Credentials
#### Scenario: User Successfully Logs In (happy path)
* **Given** I have clicked the link in the "Create Account" email
* **And** I submitted a username and strong password
* **When** I log into my account with the correct username and password
* **Then** the website logs me into my account
#### Scenario: Unsuccessful Login with Invalid Credentials (happy path)
* **Given** I navigate to the login page
* **When** I login with an invalid username or password
* **Then** the website does not let me log in

#### Scenario: User CANNOT Log In (failure)
* **Given** I have clicked the link in the "Create Account" email
* **And** I submitted a username and strong password
* **When** I log into my account with the correct username and password
* **Then** the website does not log me into my account
#### Scenario: Successful Login with Invalid Credentials (failure)
* **Given** I navigate to the login page
* **When** I login with an invalid username or password
* **Then** the website lets me log in


### US-4.6 — Users See The Correct Dashboard
#### Scenario: User Has Access To The Correct Services
* **Given** I am a user with a role other than "normal attendee"
* **When** I log into the website
* **Then** I see the pages to the services I need to access
* **And** I do not see any other services
* **And** I am not blocked from visiting any of the pages on my dashboard
#### Scenario: User Has Access To The Wrong Services
* **Given** I am a user with a role other than "normal attendee"
* **When** I log into the website
* **Then** I do not see the pages to the services I need to access
* **Or** I see services I should not have access to
* **Or** I am blocked from visiting some of the pages on my dashboard