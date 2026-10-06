Objective
Today I used my home lab to understand how to identify the WHO, WHAT and WHERE of an Azure RBAC role assignment for the Finance Team.
Scenario
I created the Finance Team group in Entra ID and assigned the group the Contributor role, scoped to a specific Azure resource. When I first created the lab, I was confused about exactly where the Finance Team group was scoped.

WHO / WHAT / WHERE
The Finance Team group is the Security Principal (WHO). The role assigned to the group is Contributor (WHAT), and the assignment is scoped to the user-assigned managed identity resource (WHERE).
I was initially confused because I thought the managed identity had another resource nested inside it. After checking the actual RBAC scope, I understood that the managed identity itself is the Azure resource that the Finance Team has Contributor access to.

Owner vs Contributor
The Owner role can manage Azure resources and assign Azure RBAC roles. The Contributor role can manage Azure resources but cannot assign Azure RBAC roles.
The role itself does not determine the scope. Both Owner and Contributor can be assigned at different scopes, such as a subscription, resource group or individual resource.

Inheritance
Inheritance means that a role assignment at a higher scope also applies to the scopes underneath it.
For example, I have the Owner role assigned at the subscription scope. Because Resource Groups and individual resources sit underneath the subscription, my Owner permissions are inherited by those resources.

PowerShell
Connect-AzAccount is used to authenticate to Azure and establish an Azure context.
Get-AzRoleAssignment is used to view Azure RBAC role assignments and helped me identify the WHO, WHAT and WHERE of an assignment.
-SignInName can be used to search for role assignments using a user's sign-in name or UPN.
-ResourceGroupName can be used to investigate role assignments associated with a specific Resource Group and its resources.
-ObjectId can be used to search for role assignments using the unique Entra Object ID of a security principal, such as a user or group.

What I Learned
- Learned the main Azure RBAC roles and the differences between Reader, Contributor and Owner.
- Learned that scope is separate from the RBAC role. A security principal can be assigned a role at different scopes depending on how the access has been configured.
- Learned how RBAC inheritance works when a role is assigned at a higher scope, such as the subscription.
- Learned different Azure PowerShell cmdlets and parameters for investigating role assignments.
- Learned how to check and compare Azure RBAC role assignments using both the Azure Portal and PowerShell.
- Learned to check the actual Scope of a role assignment instead of assuming which Azure resource the permissions apply to.
