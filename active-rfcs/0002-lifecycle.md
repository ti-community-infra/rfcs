- Feature Name: Lifecycle
- Start Date: 2020-02-23
- Reference Issues:
- Implementation PR:

# Summary

We will develop a tichi plugin called lifecycle to track the status of each Issue or PR.

# Motivation

The TiDB community currently has a large number of stale issues, some of which may have been created several years ago. Some of these issues may not be discussed and tracked because the context is lost or the author never responds.

The result is that these issues may never be fixed, but they will not be closed either. Because no one will pay attention to those issues that are already very old.

# Detailed design

## Lifecycle definition

Define several life cycles for an Issue or PR as follows:

- inactive
  - status: 10 days without any update
  - label: lifecycle/inactive
- stale
  - status: 10(inactive)+90 days without any update
  - label: lifecycle/stale
- rotten
  - status: 10(inactive)+90(stale)+30 days without any update
  - label: lifecycle/rotten
- frozen
  - status: If an Issue or PR is inactive or stale/rotten, but you want to continue tracking it, use this lifecycle and it will not be closed automatically even if there is no update for a long time
  - label: lifecycle/frozen

In addition, there are two operations, close and reopen. Rotten Issue or PR will be automatically closed after 10(inactive)+90(stale)+30(rotten)+30 days.

## Commands supported by the plugin

After defining the above lifecycle and operations, the plugin will respond to the following commands:

- [remove]-lifecycle (inactive|stale|rotten|frozen|)
- /close
- /reopen

This would allow us to use the plugin to mark the lifecycle of each issue or PR, but this would be very inefficient and silly to handle manually.

## With automatic scanning

We can combine this with the [commenter](https://github.com/kubernetes/test-infra/tree/master/robots/commenter) tool from the k8s community to scan and reply regularly.
Using this tool we can define several [prow jobs](https://github.com/kubernetes/test-infra/blob/master/config/jobs/README.md#adding-or-updating-jobs) to execute periodically, please refer to [these configurations](https://github.com/ti-community-infra/configs/blob/main/prow/jobs/ti-community-infra/org/lifecycle-periodics.yaml) for specific examples.

With the above two tools we can automate the lifecycle management and tagging. This is an [example](https://github.com/ti-community-infra/ti-community-bot/issues/135#issuecomment-782807868). (It's working, but there are problems with the lifecycle and permission definitions)

## Permission definition

We need to define the permissions for using the plugin, and since this will involve all issues and PRs, we need to control the permissions to Organization members. (For now, only reviewer and above roles will be invited to the Org)

# Drawbacks

It may lead to an increase in automated responses from bots.

# Alternatives

N/A

# Adoption strategy

N/A

# Unresolved questions

N/A

# Future possibilities

N/A
