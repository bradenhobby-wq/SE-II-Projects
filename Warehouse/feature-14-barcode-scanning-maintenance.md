# Feature: Barcode Scanning Maintenance
**Feature ID:** 14
**Branch pattern:** `feature/14-barcode-scanning-maintenance`
**Status:** Draft
**Created:** 2026-10-13
**Input:** Allows the barcode scanner to scan the barcode and perform the correct action 
**Depends on:** [Feature 14 — Barcode Scanning Maintenance](feature-14-barcode-scanning-maintenance.md)

## User Stories
### US-14.1: Scan Barcode
**As a** warehouse worker
**I want to** the system to receive the correct information when I scan barcodes
**So that** recording shipments is easier

**Priority:** P1
**Independent test:** Scan a barcode and verify that the correct information was stored in the `BarCodeScanner`. The `BarCodeScanner` actually performing the action is irrelevant for this story.
**Acceptance scenarios:** see ### US-14.1 under Acceptance
Criteria


### US-14.2: Update Inventory When Scanning Received Items
**As a** warehouse worker
**I want to** have the inventory system updated when I scan products received from a supplier
**So that** inventory can be updated quickly

**Priority:** P1
**Independent test:** Scan 5 barcodes that contain data for received shipment items. Verify that the `BillOfLading`, `SupplierOrder`, and `ReceivedOrder` were created correctly
**Acceptance scenarios:** see ### US-14.2 under Acceptance
Criteria


### US-14.3: Update Inventory When Scanning Shipped Items
**As a** warehouse worker
**I want to** have the inventory system updated when I scan products being shipped to a customer
**So that** inventory can be updated quickly

**Priority:** P1
**Independent test:** Scan 5 barcodes that contain data for a shipped customer item. Verify that the `CustomerOrder` object was created correctly.
**Acceptance scenarios:** see ### US-14.3 under Acceptance
Criteria


### US-14.4: Update Customer Order When Shipment Arrived
**As a** warehouse worker
**I want to** scan items' barcodes to record which items were received by the customer
**So that** customer orders can easily be updated for products that didn't arrive

**Priority:** P1
**Independent test:** Scan 5 barcodes that contain data for a shipped customer item in a customer order that has 6 items (so that one item is missing). Verify that the `CustomerOrder` missing shipment variable is updated.
**Acceptance scenarios:** see ### US-14.4 under Acceptance
Criteria


## Requirements
### Functional Requirements
- **FR-001**: Action ID 1 is receiving shipment from a supplier. I.e., create a `ReceivedOrder` object
- **FR-002**: Action ID 2 is sending shipment out to a customer. It creates the initial `CustomerOrder` object
- **FR-003**: Action ID 3 is updating the `CustomerOrder` object to record any missed shipping, if there is any.
- **FR-004**: Items will only be scanned when a supplier order is received, when a customer order is sent out, and when a customer order is verified
- **FR-005**: The `actionId` must be before `request`. There must be a clear seperator between them (like a bunch of asteriks) so that the system knows when the `actionId` ends and `request` starts
- **FR-005**: Values for `actionId`, `request`, and `connected` are required to create a `BarCodeScanner`.

## Key Entities
- **BarCodeScanner**: Translates the barcode into an action to perform and the data to use.
## Data Model Requirements
### `BarCodeScanner` table
| Field | Type | Rules |
|-------|------|-------|
| `actionId` | INTEGER PK | Auto-increment |
| `request` | STRING | Required |
| `connected` | BOOLEAN | Required; default false |

## Acceptance Criteria

### US-14.1 — Scan Barcode
#### Scenario: Barcode Information Received In Proper Order
* **Given** an encoded barcode exists
* **And** a barcode scanner is connected to the system
* **When** the barcode is scanned
* **Then** a `BarCodeScanner` is created with the correct data
* **And** there was a clear separator between `actionId` and `request` in the barcode data
#### Scenario: Barcode Format Missing Separator
* **Given** an encoded barcode exists
* **And** a barcode scanner is connected to the system
* **When** the barcode is scanned
* **Then** a `BarCodeScanner` is created with the correct data
* **And** the system was not able to differentiate what is `actionId` and what is `request` in the barcode data

### US-14.2 — Update Inventory When Scanning Received Items
#### Scenario: Barcode Successfully Records Received Items
* **Given** an encoded barcode exists
* **And** `actionId` is 1
* **When** the barcode is scanned by a connected barcode scanner
* **Then** the received items are recorded into a `ReceivedOrder` object
* **And** the system responds "Items successfully received"
#### Scenario: Barcode Format Incompatible With Action
* **Given** an encoded barcode exists
* **And** `actionId` is 1
* **When** the barcode is scanned by a connected barcode scanner
* **And** the system cannot parse the `result` string to record the received items due to poor formatting
* **Then** the system does not create a `ReceivedOrder` object
* **And** the system responds "Invalid format for barcode data"

### US-14.3 — Update Inventory When Scanning Shipped Items
#### Scenario: Barcode Successfully Records Shipped Items
* **Given** an encoded barcode exists
* **And** `actionId` is 2
* **When** the barcode is scanned by a connected barcode scanner
* **Then** the shipped items are recorded into a `CustomerOrder` object
* **And** the system responds "Shipped items successfully recorded"
#### Scenario: Barcode Format Incompatible With Action
* **Given** an encoded barcode exists
* **And** `actionId` is 2
* **When** the barcode is scanned by a connected barcode scanner
* **And** the system cannot parse the `result` string to record the shipped items due to poor formatting
* **Then** the system does not create a `CustomerOrder` object
* **And** the system responds "Invalid format for receiving shipments"

### US-14.4 — Update Customer Order When Shipment Arrived
#### Scenario: Barcode Successfully Updates Customer Order
* **Given** an encoded barcode exists
* **And** `actionId` is 3
* **When** the barcode is scanned by a connected barcode scanner
* **Then** the `CustomerOrder` object is updated with any missing merchandise
* **And** the system responds "Missing items successfully recorded"
#### Scenario: Barcode Format Incompatible With Action
* **Given** an encoded barcode exists
* **And** `actionId` is 3
* **When** the barcode is scanned by a connected barcode scanner
* **And** the system cannot parse the `result` string to record the shipped items due to poor formatting
* **Then** the `CustomerOrder` object is not updated
* **And** the system responds "Invalid format for updating missing shipment"