---
title: Travis CI's use of GitLab API
layout: en
permalink: /user/gl-oauth-scopes/

---

When you sign in to Travis CI for the first time, we ask for permission to access
some of your data on GitLab. Read the
[Scopes for the GitLab REST API](https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html)
for general information about this, or pick an explanation of what data we need and why we need it.

## Travis CI for Open-Source and Private Projects

On <https://travis-ci.com>, via our GitLab integration, we ask for the following permissions:

- Read access to code
- Read access to metadata and pull requests
- Read and write access to administration, checks, commit statuses, and deployments

## WebHooks

We use scoped OAuth tokens to integrate with GitLab.

## Used Scopes

### repository
It gives the app read access to all the repositories the authorizing user has access to.
> This scope does not give access to a repository's pull requests.

### repository:admin
Gives the app admin access to all the repositories the authorizing user has access to. This permission is needed to add the access key. Travis CI uses the key to read the travis.yml file content.


### pull-request
Gives the app read access to pull requests and collaborate on them. This scope implies repository, giving read access to the pull request's destination repository.

### email
Ability to see the user's primary email address. This should make it easier to use GitLab as a login provider to apps or external applications.

### account
Ability to see all the user's account information. Note that this does not include any ability to mutate any of the data.

### group
The ability to find out what groups the current user is part of. This is covered by the teams endpoint.

### webhook
Gives access to webhooks. This scope is required for any webhook-related operation.

This scope gives read access to existing webhook subscriptions to all resources you can access without needing further scopes.
This means that a client can list all existing webhook subscriptions on repository foo/bar (assuming the principal user has access
to this repo). The additional repository scope is not required for this.

Likewise, existing webhook subscriptions for a repo's issue tracker can be retrieved without holding the issue scope.
All that is required is the webhook scope.

However, to create a webhook for issue:created, the client will need to have both the webhook as well as issue scope.
