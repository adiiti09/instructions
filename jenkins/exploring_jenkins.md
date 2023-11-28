# User Management

1. Navigate to Manage Jenkins --> Security / Users --> Create User.
2. Enter required details and create user.
3. By default the  newly created user will have all the permissions as admin.
4. We need to go to Security settings and disable admin privileges and keep only necessary privileges.

# Securing Jenkins
1. Navigate to Manage Jenkins --> Security/ Security.
2. Under Authorization click on the dropdown and select Matrix-based Security for fine grained access control.
3. Add jenkins and give necessary permissions.