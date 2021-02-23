- Feature Name: Issue Helper
- Start Date: 2020-02-20
- Reference Issues:
- Implementation PR:

# Summary

We'll use GitHub Issue [contact_links](https://docs.github.com/en/github/building-a-strong-community/configuring-issue-templates-for-your-repository#configuring-the-template-chooser) to create bug reports, and in contact_links we'll put an external web page called issue-helper to help you create bug reports in a standard format.

# Motivation

In the past, TiDB's code repository used GitHub Issues to create bug reports, but because GitHub Issues use markdown to organize and write the report content. This caused our bug reports to be missing the basic information needed to reproduce the bug, making it impossible for our developers to reproduce the bug.

Also, as our bug reports require more and more information, the issue templates become more and more complex, making it difficult for users or contributors to fill out the templates.

So we can use GitHub Issue's contact_links to develop a web page to help and guide people through the process of filling out a bug report. This will help us collect bug reports in a better and more standard way and make it easier for users and contributors to fill them out.

# Detailed design

This is the bulk of the RFC. Explain the design in enough detail for somebody
familiar with TiDB community infra to understand, and for somebody familiar with the
implementation to implement. This should get into specifics and corner-cases,
and include examples of how the feature is used. Any new terminology should be
defined here.

# Drawbacks

Why should we _not_ do this? Please consider:

- implementation cost, both in term of code size and complexity
- the impact on teaching people
- integration of this feature with other existing and planned features
- cost of migrating existing applications (is it a breaking change?)

There are tradeoffs to choosing any path. Attempt to identify them here.

# Alternatives

What other designs have been considered? What is the impact of not doing this?

# Adoption strategy

Is this a breaking change? How will this affect other projects in the TiDB community infra ecosystem?

# Unresolved questions

Optional, but suggested for first drafts. What parts of the design are still
TBD?

# Future possibilities

Think about what the natural extension and evolution of your proposal would
be and how it would affect the project as a whole in a holistic
way. Try to use this section as a tool to more fully consider all possible
interactions with the project in your proposal.
Also consider how this all fits into the roadmap for the project
and of the relevant team.

This is also a good place to "dump ideas", if they are out of scope for the
RFC you are writing but otherwise related.

If you have tried and cannot think of any future possibilities,
you may simply state that you cannot think of anything.

Note that having something written down in the future-possibilities section
is not a reason to accept the current or a future RFC; such notes should be
in the section on motivation or rationale in this or subsequent RFCs.
The section merely provides additional information.
