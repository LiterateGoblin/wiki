---
title: AWS Identity and Access Management (IAM)
---

AWS Identity and Access Management (IAM) is the AWS service used to manage permissions between AWS services. The primary entities that grant identities permissions are users, roles, and groups. Sets of permissions are held in documents called *policies*.

## Concepts

### Users

Users map to individuals in an organization, regardless of the duties they perform. Policies can be attached to users, but the best practice is to allow users to assume roles with the permissions they need instead.

### Groups

Groups are collections of users that all perform a similar role. A policy can be attached to a group to give all users in that group the same permissions.

### Roles

Roles are sets of permissions that can temporarily apply to a user or service in a session-based manner - the action of entering a session with these permissions is called "assuming" the role. AWS's recommendation for security is to give users and groups few permissions, but instead grant them permission to assume the necessary roles to perform their job function.

Policies are attached to roles to define the permissions that would be granted to an identity assuming them.

## Identity-based and resource-based policies

The policies that can be attached to users, groups, and roles are identity-based - that is, they define what some identity is allowed to do to other resources. Some AWS resources also feature the ability to attach a policy to them. These policies are called resource-based policies. This kind of policy instead defines what can be done to the attached resources, and who is allowed to do those actions.

## References

[^1]: "Creating and Managing IAM Users." "Managing MySQL Security and User Access." *AWS Skill Builder*, [**explore.skillbuilder.aws/learn/course/8033/play/26696/managing-mysql-security-and-user-access**](https://explore.skillbuilder.aws/learn/course/8033/play/26696/managing-mysql-security-and-user-access). Accessed 23 Dec 2023.
