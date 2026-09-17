## Acceptance Criteria

### US-3.1 — Mark People Present
#### Scenario: Successfully Marked Attendees Present
* **Given** I am a bible teacher logged into the website
* **And** I navigate to the "Record Attendance"page
* **When** I mark people down as present
* **Then** the website does display a message like "Attendance successfully recorded"
* **And** the website does go to the "Past Attendance" page
* **And** today's class attendance is recorded among the past classes
#### Scenario: Class Attendance not recorded
* **Given** I am a bible teacher logged into the website
* **And** I navigate to the "Record Attendance"page
* **When** I mark people down as present
* **Then** the website does not display a message like "Attendance successfully recorded"
* **And** the website does not go to the "Past Attendance" page
* **And** today's class attendance is not recorded among the past classes

### US-3.2 — See Past Attendance Per Class
#### Scenario: Past Attendance Totals Listed
* **Given** I am a bible teacher logged into the website
* **When** I navigate to the "Past Attendance" page
* **Then** the attendance totals of previous classes are displayed
#### Scenario: Past Attendance Totals Not Shown
* **Given** I am a bible teacher logged into the website
* **When** I navigate to the "Past Attendance" page
* **Then** the attendance totals of previous classes are not displayed

### US-3.3 — See Past Attendance Lists
#### Scenario: Past Attendance List Shown
* **Given** I am a bible teacher logged into the website
* **And** I navigate to the "Past Attendance" page
* **When** I click on the dropdown arrow by a class
* **Then** the website shows who attended that class
#### Scenario: Past Attendance List Not Displayed
* **Given** I am a bible teacher logged into the website
* **And** I navigate to the "Past Attendance" page
* **When** I click on the dropdown arrow by a class
* **Then** the website does not show who attended that class

### US-3.4 — See Bible Class Attendees' General Information
#### Scenario: Attendees' General Information Viewable
* **Given** I am a bible teacher logged into the website
* **And** I navigate to the "Past Attendance" page
* **And** I click on the dropdown arrow by a class
* **When** I click on the name of someone who attended the class
* **Then** I can see their general information (assuming they have any recorded)
#### Scenario: Attendees' General Information Not Shown
* **Given** I am a bible teacher logged into the website
* **And** I navigate to the "Past Attendance" page
* **And** I click on the dropdown arrow by a class
* **When** I click on the name of someone who attended the class
* **Then** I do not see their general information (assuming they have any recorded)

### US-3.5 — See Bible Class Attendees' Attendance History
#### Scenario: Attendees' Attendance History Viewable
* **Given** I am a bible teacher logged into the website
* **And** I navigate to the "Past Attendance" page
* **And** I click on the dropdown arrow by a class
* **When** I click on the name of someone who attended the class
* **Then** I can see the full list of dates they attended bible class, from most recent to oldest
#### Scenario: Attendees' Attendance History Not Shown
* **Given** I am a bible teacher logged into the website
* **And** I navigate to the "Past Attendance" page
* **And** I click on the dropdown arrow by a class
* **When** I click on the name of someone who attended the class
* **Then** I can see the full list of dates they attended bible class, from most recent to oldest

### US-3.6 — User Staff Adds Bible Classes
#### Scenario: Attendees' Attendance History Viewable
* **Given** I am a bible teacher logged into the website
* **And** I navigate to the "Past Attendance" page
* **And** I click on the dropdown arrow by a class
* **When** I click on the name of someone who attended the class
* **Then** I can see the full list of dates they attended bible class, from most recent to oldest
#### Scenario: Attendees' Attendance History Not Shown
* **Given** I am church staff with admin priveleges and am logged into the website
* **And** I navigate to the "Roles Management" page
* **When** I add a Bible Class
* **Then** the bible class teacher gets access to their class attendance