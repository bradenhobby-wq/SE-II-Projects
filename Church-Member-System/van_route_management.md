# Feature: <Van Route Management>
**Feature ID:** 1
**Branch pattern:** `feature/van_route_management`
**Status:** Draft
**Created:** 2026-09-11
**Input:** Church Van drivers need to have reliable access to routes.
**Depends on:** [Feature 2]
---

**Priority:** P1
**Independent test:** Have the appropriate church staff view and edit the church van driver list on the mobile app
**Acceptance scenarios:** see ### US-N.1 under Acceptance
Criteria

### US-N.1: See Available Drivers
**As a** member of the church staff
**I want to** be able to access and modify the volunteer church van drivers list
**So that** I can have a church van driver ready every Sunday

**Priority:** P2
**Independent test:** Have the current church van driver view the pick-up list
**Acceptance scenarios:** see ### US-N.2 under Acceptance
Criteria

### US-N.2: See Pick-up List
**As a** church van driver
**I want to** be able to see the names and addresses of the kids I am picking up
**So that** I can pick up all of the kids on time

---
### Functional Requirements
- **FR-001**: Both the church van driver list and the pick-up list must be modifiable.
- **FR-002**: Only the appropriate church staff can log in and modify the lists.
- **FR-003**: Only the current church van driver can log in and view the pick-up list.
---

## Key Entities
- **Registered Church Member**: person who's contact info, name, and other information is logged in the database
- **Pick-up List**: List of children, with their home address, to pick up for church
- **Church Van Drivers**: List of church members who are able to drive the bus

## Data Model Requirements
### `church van drivers` table
| Field | Type | Rules |
|-------|------|-------|
| `name` | STRING(100)| Required, unique; stored lowercase |
| `phoneNumber` | INTEGER PK | Auto increment |
| `currentDriver` | BOOLEAN | Required |
| … | … | … |
### `Pick-up List` table
| Field | Type | Rules |
|-------|------|-------|
| `name` | STRING(100) |  Required, unique; stored lowercase |
| `address` | STRING(100) |  Required, unique; stored lowercase |
| … | … | … |


## Acceptance Criteria

### US-N.1: See Available Drivers

#### Scenario: Descriptive name (happy path)
* **Given** I am the secretary for the church
* **When** I need to figure out who is driving the church van this Sunday
* **Then** I need to see a list of available drivers and their contact info

#### Scenario: Descriptive name (failure / edge)
* **Given** … I do not work for the church
* **When** … I log into the mobile app
* **Then** … I should not see the names and contact info of all the normal drivers.

### US-N.2: See Pick-up List

#### Scenario: Descriptive name (happy path)
* **Given** I am the current church van driver for the church
* **When** I am logging into the mobile app
* **Then** I need to be able to see the name and address of the kids I am picking up.

#### Scenario: Descriptive name (failure / edge)
* **Given** … I am not the current church van driver for the church
* **When** … I log into the mobile app
* **Then** … I should not see the list of children on the bus route.