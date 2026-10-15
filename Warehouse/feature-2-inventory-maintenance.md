# Feature: Inventory Maintenance
**Feature ID:** 2
**Branch pattern:** `feature/inventory_maintenance`
**Status:** Draft
**Created:** 2026-09-27
**Input:** Maintain inventory in the warehouse - add, update, delete, order more - with a list of products and items (which are the products currently in stock)
**Depends on:** [Feature 1 - Common Inventory Items Management] (feature-1-common-inventory-items.md)

## User Stories
### US-2.1: Add Items to Inventory
**As a** Inventory clerk
**I want to** be able to add products to the inventory list
**So that** we can know which items are in stock

**Priority:** P1
**Independent test:** Navigate on the UI to the page where you add items to inventory and add new items
**Acceptance scenarios:** see ### US-2.1 under Acceptance
Criteria

### US-2.2: Search for Items in Inventory
**As a** Inventory clerk
**I want to** be able to search for items in inventory
**So that** I can access their information

**Priority:** P1
**Independent test:** Search for an item based on an attribute and view its information
**Acceptance scenarios:** see ### US-2.2 under Acceptance
Criteria

### US-2.3: Edit Items in Inventory
**As a** Inventory clerk
**I want to** be able to edit items in inventory
**So that** the inventory data is up-to-date

**Priority:** P1
**Independent test:** Search for an item, edit its information
**Acceptance scenarios:** see ### US-2.2 under Acceptance
Criteria

### US-2.4: Delete Items in Inventory
**As a** Inventory clerk
**I want to** have the system automatically delete products from the inventory list when a product's in stock value equals zero
**So that** the inventory data only displays products in stock

**Priority:** P1
**Independent test:** Search for an item, change it's in stock number to zero, watch the item get removed from the inventory list
**Acceptance scenarios:** see ### US-2.3 under Acceptance
Criteria

### US-2.5: Update Inventory When Scanning Items
**As the** warehouse worker
**I want to** update inventory when I scan an item when its received/shipped out
**So that** the inventory data is automatically updated when the inventory is received

**Priority:** P1
**Independent test:** Scan items for shipment and receiving. Make sure that the inventory is properly increased for receiving and propery decreased for shipment
**Acceptance scenarios:** see ### US-2. under Acceptance
Criteria

## Requirements
### Functional Requirements
- **FR-001**: System MUST not have any duplicate serial numbers
- **FR-002**: An Item MUST include an inventory slot, serial number, aisle number, and a reference to a Product object
- **FR-003**: When searching for an item, the options for attributes to search by MUST only include the SKU, UPC, serial number, or name. These are all found in the Product object "product"
- **FR-004**: When clicking on an item that shows up in the search, all of the item's attributes should be displayed
- **FR-005**: System MUST allow authorized employees to add, update, or delete the Inventory List
- **FR-006**: System MUST group all Items with the same Product together unless the serial number is specified in the search
- **FR-007**: When an Item is created, the Product attribute "inventoryCount" MUST be updated. This attribute must be Static so that every instance has the accurate inventoryCount
- **FR-008**: search results MUST appear before 10 seconds have passed from the search query

## Key Entities
- **Item**: While a Product is a description of a possible inventory item, an Item represents an individual package. An Item will be created every time a product is received.
## Data Model Requirements
### `InventoryItems` table
| Field | Type | Rules |
|-------|------|-------|
| `items` | ITEM LIST |Required, mutable |
### `Item` table
| Field | Type | Rules |
|-------|------|-------|
| `inventorySlot` | STRING(50) |Required, unique |
| `aisleNumber` | INTEGER | Required |
| `serialNumber` | STRING(50) | Required, unique |
| `product` | PRODUCT | Required |

## Acceptance Criteria

### US-2.1 — Add Items to Inventory
#### Scenario: Item Successfully Added
* **Given** An inventory clerk is authorized
* **And** a product exists
* **When** the clerk enters an item specifying the product, serial number, and inventory slot
* **Then** the inventory list updates correctly
#### Scenario: Clerk cannot add Item with existing Serial Number
* **Given** An inventory clerk is authorized
* **When** the clerk enters an item specifying the product, serial number, and inventory slot
* **And** the serial number is already used
* **Then** the system throws 'DuplicateException'

### US-2.2 — Search for Items in Inventory
#### Scenario: Can Search for Items
* **Given** an inventory clerk is authorized
* **And** an item exists
* **When** the clerk searches for the item using correct information
* **Then** only the correct item should be displayed
* **And** more information shows up when the item is clicked

### US-2.3 — Edit Items in Inventory
#### Scenario: Item Successfully Updated
* **Given** an inventory clerk is authorized and an item exists
* **When** the clerk edits the item's information
* **Then** the inventory list shows the correct item information
#### Scenario: Clerk cannot change item to an in-use serial number
* **Given** the inventory clerk is authorized and an item exists
* **When** the clerk edits the item's information, changing the serial number of the product
* **And** the serial number is already in use
* **Then** the system throws 'DuplicateException'

### US-2.4 — Delete Items in Inventory
#### Scenario: Clerk deletes item
* **Given** an inventory clerk is authorized and an item exists
* **When** the clerk deletes an item
* **Then** item is removed from the inventory list

### US-2.5 — Update Inventory When Scanning Items
#### Scenario: Warehouse worker scans received item into inventory slot
* **Given** a warehouse worker is authorized and an item exists
* **When** the worker scans the item being received
* **Then** an item is created with the inventory count of its Product class is incremented by one
* **And** the inventory slot is determined by the system and a serial number is generated
#### Scenario: Warehouse worker scans shipped item out
* **Given** a warehouse worker is authorized and an item exists
* **When** the worker scans the item being shipped
* **Then** the item is deleted and the inventory count of its Product class is decremented by one
* **And** the inventory slot is determined by the system and a serial number is generated