## Acceptance Criteria

### US-1.1: See Available Drivers

#### Scenario: Church Staff Views Driver List
* **Given** I am logged onto the website as authorized church staff
* **When** I click on the "Drivers" page
* **Then** I see a list of available drivers with their name and phone number displayed

#### Scenario: Church Staff Cannot view Driver List
* **Given** I am logged onto the website as authorized church staff
* **When** I navigate to the "Drivers" page
* **Then** I do not see a list of available drivers with their name and phone number displayed

### US-1.2: Edit Available Drivers

#### Scenario: Church Staff Edits Driver List
* **Given** I am logged onto the website as authorized church staff
* **And** I navigate to the "Drivers" page
* **And** I edit the Drivers List
* **When** I save my changes
* **Then** The website does display a message like "Drivers list successfully updated"
* **And** The "Drivers" page displays the updated list

#### Scenario: Church Staff Cannot Edit Driver List
* **Given** I am logged onto the website as authorized church staff
* **And** I navigate to the "Drivers" page
* **And** I edit the Drivers List
* **When** I save my changes
* **Then** The website does not display a message like "Drivers list successfully updated"
* **Or** The "Drivers" page does not display the updated list

### US-1.3: See Pick-up List

#### Scenario: Van Driver Views Pick-up List
* **Given** I am the current van driver or staff member of the church
* **And** I am logged onto the website
* **When** I navigate to "Pick-up List" page
* **Then** I see the names and address of the kids I am picking up.

#### Scenario: Van Driver Cannot View Pick-up List
* **Given** I am not the current church van driver for the church
* **And** I am logged onto the website
* **When** I navigate to "Pick-up List" page
* **Then** I do not see the name and address of the kids I am picking up

### US-1.4: Edit Pick-up List

#### Scenario: Church Staff Edits Pick-up List
* **Given** I am the current van driver or staff member of the church
* **And** I am logged onto the website
* **And** I navigate to "Pick-up List" page
* **And** I edit the Pick-up-List
* **When** I click "Save"
* **Then** The website does display a message like "Pick-up list successfully updated"
* **And** The "Pick-up" page does display the updated list

#### Scenario: Van Driver Cannot View Pick-up List
* **Given** I am not the current church van driver for the church
* **And** I am logged onto the website
* **And** I navigate to "Pick-up List" page
* **And** I edit the Pick-up-List
* **When** I click "Save"
* **Then** The website does not display a message like "Pick-up list successfully updated"
* **Or** The "Pick-up" page does not display the updated list