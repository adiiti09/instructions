# User Management

1. Navigate to Manage Jenkins --> Security / Users --> Create User.
2. Enter required details and create user.
3. By default the  newly created user will have all the permissions as admin.
4. We need to go to Security settings and disable admin privileges and keep only necessary privileges.

# Securing Jenkins
1. Navigate to Manage Jenkins --> Security/ Security.
2. Under Authorization click on the dropdown and select Matrix-based Security for fine grained access control.
3. Add jenkins and give necessary permissions.

# Plugin Management
1. Navigate to Manage Jenkins --> System COnfiguration / Plugins.

## Updates
> Shows any updates to already installed plugins.

## Available Plugins
> List of plugins that are available to be installed

## Installed Plugins
> List of plugins that are already installed

## Advanced Settings
> - Proxy settings that can be specified in case your jenkins installation is behind a proxy
> - Custom plugins that can be uploaded or accessed from some URL