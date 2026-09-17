## Key Entities
- **Church Attendee**: Someone who goes to the church and has submitted general information. It cannot be deleted, but it can be updated.

## Data Model Requirements
### `churchAttendee` table
| Field | Type | Rules |
|-------|------|-------|
| `churchId` | INTEGER | Required, randomize upon generation |
| `fullName` | STRING (255) | Required, Default '' |
| `homeAddress` | STRING(100) | Required, Default '' |
| `phoneNumber` | INTEGER | Default 0 |
| `email` | STRING(100) | Default '' |
| `churchRole` | STRING(255) | Required, Default 'normal attendee' |
| `hasKids` | BOOLEAN | Default 'false' |
| `schoolOfKids` | STRING(100) | Not required |
| `bibleClassAttendance` | STRING(100) ARRAYLIST | Required; in format MM/DD/YYYY; Default null |
| `immediateFamilyMembers` | STRING(100) | Required; Default '' |