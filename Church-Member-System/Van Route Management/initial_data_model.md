## Key Entities
- **Registered Church Member**: person who's contact info, name, and other information is logged in the database
- **Pick up List**: List of children, with their home address, to pick up for church. Retrieve the necessary info from their churchAttendee profile if they have one
- **Van Drivers**: List of church members who are able to drive the bus. Retrieve the necessary info from their churchAttendee profile

## Data Model Requirements
### `vanDrivers` table
| Field | Type | Rules |
|-------|------|-------|
| `name` | STRING(100)| Required, unique; stored lowercase |
| `phoneNumber` | INTEGER PK | Auto increment |
| `currentDriver` | BOOLEAN | Required |

### `pickUpList` table
| Field | Type | Rules |
|-------|------|-------|
| `name` | STRING(100) |  Required, unique; stored lowercase |
| `address` | STRING(100) |  Required, unique; stored lowercase |
| `pickUpSunday` | BOOLEAN | Required; Default "true" |