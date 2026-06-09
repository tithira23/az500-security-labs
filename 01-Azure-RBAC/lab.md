# Lab 01 – Azure RBAC

## Objective

Implement Azure Role-Based Access Control using the principle of least privilege.

## Scenario

A test user requires read-only access to an Azure resource group. The user should be able to view resources but must not be able to create, modify, or delete resources.

## Azure Services Used

- Microsoft Entra ID
- Azure RBAC
- Resource Groups
- Azure Portal

## Steps Completed

1. Created a resource group named `rg-az500-rbac-lab`.
2. Selected a test user from Microsoft Entra ID.
3. Assigned the Reader role at the resource group scope.
4. Verified the role assignment under Access Control IAM.
5. Tested access restriction by attempting a privileged action.
6. Confirmed that the test user had read-only access only.

## Evidence Captured

Screenshots are stored in the `screenshots` folder.

- `01-resource-group-created.png`
- `02-test-user-selected.png`
- `03-reader-role-assigned.png`
- `04-access-control-iam-view.png`
- `05-permission-denied-test.png`

## Security Concept

This lab demonstrates the principle of least privilege. The Reader role allows visibility into Azure resources but does not allow modification, deletion, or privileged administrative actions.

## Outcome

The Reader role was successfully assigned to the test user at the resource group scope. Access verification confirmed that the user could view resources but could not perform administrative changes.