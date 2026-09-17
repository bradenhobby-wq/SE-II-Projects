## Key Entities
- **Bible Class**: Will contain an arrayList of churchAttendees. 
## Data Model Requirements
### `bibleClass` table
| Field | Type | Rules |
|-------|------|-------|
| `presentMembers` | CHURCHATTENDEE ARRAYLIST | Required |
| `className` | STRING(255) | Required |
| `teacherID` | INTEGER | Required, matches `churchID` of teacher |