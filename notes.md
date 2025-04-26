# 🗓️ Notes: April 20, 2025

## Roles and Role Binding
- Role : Resource + Permissions
- Login - Authentication
- Role - Authorisation

## K8s
- Permissions/Verbs for k8s resources
    - Cretate
    - Read (list, get, watch)
    - Update
    - Patch
    - Delete
- Roles
    - [Resources] + [Verbs] + [Namespace]
- RoleBinding
    - [Role] + [User/Group/SA] + [Namespace]

## Application Onboarding into k8s Cluster:
- Create a namespace
- Set the Quota for the namespace
- Role and Role Binding for namespace
- Deploying Resources in namespace

## Super Admin 
- They will handle the jobs like Applications onboarding to the cluster

## Cluster Administrators
- Cluster Role : Resources + Permissions
- Cluster Role Binding : Cluster Role + User/Group/SA

Cluster Roles are not tied with namespaces