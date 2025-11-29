# Lab02a - Manage Subscriptions and RBAC

- Task 1: Implement management groups
  - Management Groups > Create
- Task 2: Review and assign a built-in Azure role
  - Management Groups > Access Control > Add Role Assignment
- Task 3: Create a custom RBAC role
  - Management Groups > Access Control > Add Custom Role
 
```json
{
    "properties": {
        "roleName": "Custom Support Request",
        "description": "A custom contributor role for support requests.",
        "assignableScopes": [
            "/providers/Microsoft.Management/managementGroups/az104-mg1"
        ],
        "permissions": [
            {
                "actions": [
                    "Microsoft.Authorization/*/read",
                    "Microsoft.Resources/subscriptions/resourceGroups/read",
                    "Microsoft.Support/*"
                ],
                "notActions": [
                    "Microsoft.Support/register/action"
                ],
                "dataActions": [],
                "notDataActions": []
            }
        ]
    }
}
```
- Task 4: Monitor role assignments with the Activity Log
  - Activity Log
