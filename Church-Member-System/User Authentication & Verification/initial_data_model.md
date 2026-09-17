## Key Entities
- **User Profile**: Contains a churchAttendee object and needs to use get methods to access private variables in churchAttendee
- **Sessions**: Allows a user to stay signed in while navigating across multiple pages and needs to use get methods to access private variables in userProfile
## Data Model Requirements
### `userProfile` table
| Field | Type | Rules |
| `id` | INTEGER PK | Required, references `churchAttendee.churchId` |
| `role` | STRING(255) | Required, references `churchAttendee.churchRole` |
| `username` | STRING(100) | Required, unique |
| `password` | STRING(255) | Required, bycryt hash only
| `generalInfo` | CHURCHATTENDEE | Required |

### `sessions` table
| Field | Type | Rules |
| `id` | INTEGER PK | Auto-increment |
| `token` | STRING(255) | Required |
| `user` | USER PROFILE | Required; used especially to access "role" and "id" for verification |
| `active` | BOOLEAN | Required; shows if the session is still valid |
| `lastAccessed` | STRING(255) | Equals current timestamp until the user stops accessing the website |