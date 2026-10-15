# Feature: Common Inventory Items Management
**Feature ID:** 1
**Branch pattern:** `feature/common_inventory_items_management`
**Status:** Draft
**Created:** 2026-10-01
**Input:** Maintain items that are commonly purchased for inventory - includes identifying attributes like identifaction codes, price, and product descriptions
**Depends on:** [Feature 3 — User Authentication and Verification](feature-3-user-authentication-and-verification.md)

## User Stories
### US-1.1: Add Common Inventory Items
**As a** inventory clerk
**I want to** easily add information about inventory items that we commonly purchase
**So that** ordering new inventory is simpler

**Priority:** P1
**Independent test:** Clerk calls `Product.add`with all required variables; Clerk calls `CommonItems.add` with the created product, product appears in `CommonItems.list`
**Acceptance scenarios:** see ### US-1.1 under Acceptance
Criteria

### US-1.2: Edit Common Inventory Items
**As a** inventory clerk
**I want to** easily edit information about inventory items that we frequently purchase
**So that** inventory orders use up-to-date information

**Priority:** P1
**Independent test:** Clerk calls `Product.edit` with the variables they want to change; edits appear in `CommonItems.list`
**Acceptance scenarios:** see ### US-1.2 under Acceptance
Criteria

### US-1.3: Delete Common Inventory Items
**As a** inventory clerk
**I want to** delete inventory items that we no longer purchase from the list
**So that** the common inventory list isn't too cluttered

**Priority:** P1
**Independent test:** Clerk calls `Product.delete` with the product they want to delete; product no longer appears in `CommonItems.list`
**Acceptance scenarios:** see ### US-1.3 under Acceptance
Criteria

### US-1.4: Search Products By Name or UPC
**As a** inventory clerk or shipping clerk
**I want to** be able to easily find the information of a certain product
**So that** I can access product information when I need to

**Priority:** P1
**Independent test:** Clerk calls `CommonItems.search` with a name; products in `CommonItems.list` with a matching (or similar) name show up
**Acceptance scenarios:** see ### US-1.4 under Acceptance
Criteria

## Requirements
### Functional Requirements
- **FR-001**: Authorized workers MUST be able to access all of the CommonItems functions
- **FR-002**: The sku and upc MUST be unique on every instance
- **FR-003**: minStock MUST be less than maxStock
- **FR-004**: salesPrice MUST be rounded to two decimal places when displayed
- **FR-005**: search results MUST appear before 10 seconds have passed from the search query

## Key Entities
- **CommonItems**: Contains a list of Products. Is meant to provide quick access to products commonly purchased
- **Product**: Description of an item that the warehouse might purchase.
## Data Model Requirements
### `Product` table
| Field | Type | Rules |
|-------|------|-------|
| `minStock` |INTEGER | Required |
| `maxStock` |INTEGER | Required |
| `currentStock` |INTEGER | Required |
| `sku` | STRING(30) | Required, unique |
| `upc` | STRING(30) | Required; unique |
| `name` | STRING(30) | Required; unique |
| `salesPrice` | DOUBLE | Required |
| `primarySupplier` | SUPPLIER | Required |

### `CommonItems` table
| Field | Type | Rules |
|-------|------|-------|
| `products` | PRODUCT LIST | Required |
| `productCount` | INTEGER | Auto-increment with additions to `products` |


## Acceptance Criteria

### US-1.1 — Add Common Inventory Items
#### Scenario: Product Successfully Added
* **Given** An inventory clerk is logged in and authorized
* **When** they submit a request to add a `Product` to `CommonItems` with all of the required fields filled in
* **Then** the system responds "Product successfully added"
* **And** the product's information is saved to `CommonItems`
#### Scenario: System Doesn't Allow Duplicate SKUs or UPCs
* **Given** An inventory clerk is logged in and authorized
* **When** they try to add a `Product` with a SKU or UPC that is already in use
* **Then** the system does not allow the `Product` to be created
* **And** the system responds "SKU or UPC already in use"

### US-1.2 — Edit Common Inventory Items
#### Scenario: Edits on Item Saved
* **Given** An inventory clerk is logged in and authorized
* **When** they save changes to a `Product`
* **Then** the changes are saved on the `CommonItems` page
* **And** the system responds "Product successfully saved"
#### Scenario: System Doesn't Allow Duplicate SKUs or UPCs
* **Given** An inventory clerk is logged in and authorized
* **When** they try to edit a `Product` to a SKU or UPC that is already in use
* **Then** the system does not allow the `Product` to be changed
* **And** the system responds "SKU or UPC already in use"

### US-1.3 — Delete Common Inventory Items
#### Scenario: Item Successfully Deleted
* **Given** An inventory clerk is logged in and authorized
* **When** they delete a `Product`
* **Then** the `Product` no longer appears on the `CommonItems` page
* **And** the `Product` is not saved in memory

### US-1.4 — Search Products By Name or UPC
#### Scenario: Product Shows Up When Searched By Name Verbatim
* **Given** an inventory clerk or shipping clerk is logged in and authorized
* **When** they search for a `Product` by name verbatim
* **Then** that `Product` is at the top of the search results
#### Scenario: Search Results Accurate With Incomplete Search
* **Given** an inventory clerk or shipping clerk is logged in and authorized
* **When** they search for a `Product` by name with one word missing
* **Then** that `Product` is near/at the top of the search results
#### Scenario: Search Results Empty When No Matching Product Name
* **Given** an inventory clerk or shipping clerk is logged in and authorized
* **When** they search for a `Product` by name using a random phrase not related to a product (like "brussell sprouts")
* **Then** the search results are empty
* **And** the system responds "No matching product"
#### Scenario: Product Shows Up When Searched By UPC
* **Given** an inventory clerk or shipping clerk is logged in and authorized
* **When** they search for a `Product` by UPC
* **Then** that `Product` is at the top of the search results
#### Scenario: Search Results Empty When No Matching Product UPC
* **Given** an inventory clerk or shipping clerk is logged in and authorized
* **When** they search for a `Product` by UPC using a UPC not in use
* **Then** the search results are empty
* **And** the system responds "No matching product"