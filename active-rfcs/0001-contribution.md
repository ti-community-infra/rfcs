- Feature Name: Contribution
- Start Date: 2021-03-01
- Reference Issues:
- Implementation PR:

# Summary

A contribution plugin will be developed for tichi, which is mainly responsible for labeling external members' PRs with `contribution` or `first-time-contributor` labels.

# Motivation

We need to distinguish between internal and external contributor PRs, and prioritize help with external contributor PRs, especially first-time contributor PRs, which will allow external contributors to have a good contribution experience.

# Detailed design

## contribution

For external contributors, we will label their PR with `contribution`.

### Definition:

- Label Name: `contribution`
- Usage: External Contributors
  - We will determine if it is an external contributor by whether it is an org member or not.
- Available API: https://github.com/kubernetes/test-infra/blob/9b84ac948f6eb781a318fa431d547e577ee668e4/prow/github/client.go#L67

## first-time-contributor

In addition, if the external contributor is a first-time contributor, we need to tag not only `contribution` but also `first-time-contributor`.

### Definition:

- Label Name: `first-time-contributor`
- Usage: First contribution
  - We will determine if it is a first-time contribution based on the [author_association](https://docs.github.com/en/graphql/reference/enums#commentauthorassociation) field of the PR.
- Available API: https://github.com/kubernetes/test-infra/pull/21066

## Auto-response

In addition to adding these labels, we also want to take into account that we may need to automatically reply to some external contributors' PRs with help documentation and code implementation specifications. So we add a message field to the configuration, if it is empty then we don't need to reply, otherwise we reply the message to the PR after adding these labels.

# Drawbacks

N/A

# Alternatives

N/A

# Adoption strategy

N/A

# Unresolved questions

N/A

# Future possibilities

N/A
