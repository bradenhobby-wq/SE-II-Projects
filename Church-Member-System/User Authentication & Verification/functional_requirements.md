## Requirements
### Functional Requirements
- **FR-001**: Normal users only get access to pages with normal information about church. Church staff and van drivers get access to their necessary functions, which has more sensitive information.
- **FR-002**: Users MUST authenticate with username + password
- **FR-003**: Passwords must be at least 12 characters long with at least one number, uppercase letter, lowercase letter, and special symbol
- **FR-004**: A session is created upon login and is required to stay logged in
- **FR-005**: Session lifetime MUST be three hours after last access

- **FR-006**: The correct role is required to access all non-public paths
- **FR-007**: If cookies are used for sensitive variables like 'user.role' or 'session.active', they should be accessible through Inspect Mode.
- **FR-008**: No info, even the name, of sensitive variables should be accessible through Inspect Mode
- **FR-009** No sensitive info about the source code should be left in comments accessible through Inspect Mode
- **FR-010** Only required HTML should be visible on the client-side. Any references to the source code in the HTML code should not be accessible by any user
