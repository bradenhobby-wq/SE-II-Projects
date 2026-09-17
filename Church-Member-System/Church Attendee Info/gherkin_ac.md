## Acceptance Criteria

### US-2.1 — Update General Information
#### Scenario: New Member Successfully Updated General Information
* **Given** I am a new church attendee who fills out the form
* **When** I click submit on the form
* **Then** the server at the church creates a new churchAttendee object with my general information.

#### Scenario: General Information Not Stored/Stored Incorrectly
* **Given** I am a new church member who fills out the form
* **When** I click submit on the form
* **Then** my general information is not stored on the database or the information is not what I filled out.

### US-2.2 — Church Staff Views Church Member's/Guest's General Information
#### Scenario: Church Staff Can View the Member's General Information
* **Given** I am a member of the church staff who needs to see a member's general information
* **And** I search the member on the database
* **When** I click "Edit" under their profile
* **Then** the member's general information is visible.
#### Scenario: General Information Not Viewable
* **Given** I am a member of the church staff who needs to see a member's general information
* **And** I search the member on the database
* **When** I click "Edit" under their profile
* **Then** the member's general information is not visible.

### US-2.3 — Church Staff Edits Church Member's General Information
#### Scenario: General Information of a Guest Successfully Updated
* **Given** I am a member of the church staff who has logged into the website
* **And** I go to the "Members" page
* **And** I edit a profile
* **When** I save my changes
* **Then** the system outputs a message like "Member info successfully saved"
* **And** the system returns to the "Members" page
* **And** the "Members" page displays the updated general information
#### Scenario: General Information Incorrectly Updated
* **Given** I am a member of the church staff who has logged into the website
* **And** I go to the "Members" page
* **And** I edit a profile
* **When** I save my changes
* **Then** the system does not output a message like "Member info successfully saved"
* **Or** the system does not return to the "Members" page
* **Or** the "Members" page does not display the updated general information