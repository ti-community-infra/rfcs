- Feature Name: Issue Helper
- Start Date: 2020-02-20
- Reference Issues:
- Implementation PR:

# Summary

We'll use GitHub Issue [contact_links](https://docs.github.com/en/github/building-a-strong-community/configuring-issue-templates-for-your-repository#configuring-the-template-chooser) to create issues, and in contact_links we'll put an external web page called issue-helper to help us create issues in a standard format.

# Motivation

In the past, TiDB's code repository used GitHub Issues to create bug reports, but because GitHub Issues use markdown to organize and write the report content. This form is simple but not structured, and not easy to use, so information transmission is inefficient.

Also, as our bug reports require more and more information, the issue templates become more and more complex, making it difficult for users or contributors to fill out the templates.

So we can use GitHub Issue's contact_links to develop a web page to help and guide people through the process of filling out a bug report. This will help us collect bug reports in a better and more standard way and make it easier for users and contributors to fill them out.

# Detailed design

## Introducing GitHub Issue contact_links

GitHub Issues provides a way to configure external links. We can use the following configuration to add an external contact link.

```yaml
// .github/ISSUE_TEMPLATE/config.yml
blank_issues_enabled: false
contact_links:
  - name: Create new issue
    url: https://prow.tidb.io/tichi/new-issue
    about: Please use the following link to create a new issue.
```

The effect of using this feature can be seen in the [vuejs repository](https://github.com/vuejs/vue/issues/new/choose).

## External contact links combined with GitHub Issues

Once we enable external links, we can direct the user or contributor to a web page that we've developed, where we'll use a standard form for the user or contributor to fill out the report, and then we'll use the [GitHub Issue creation API](https://docs.github.com/en/github/managing-your-work-on-github/about-automation-for-issues-and-pull-requests-with-query-parameters#supported-query-parameters) to resubmit the form to GitHub and create the Issue.

The API looks like this: https://github.com/pingcap/tidb/issues/new?title=example&body=FormContent

## TiDB Issue Helper

The main issues we need to focus on in TiDB are divided into two categories, one is [Bug Report](https://github.com/pingcap/tidb/blob/master/.github/ISSUE_TEMPLATE/bug-report.md) and the other is [New Feature Request](https://github.com/pingcap/tidb/blob/master/.github/ISSUE_TEMPLATE/feature-request.md).

So our Issue Helper focuses on these two types of reports and develops forms for them and then fills them back into the GitHub Issue.

### Bug Report Template

```md
### Steps to reproduce

### What is expected?

### What is actually happening?

### Any additional comments? (optional)

| Environment   | Info   |
| ------------- | ------ |
| TiDB Version  | v4.0.1 |
| MySQL Version | 8.0.19 |

<!-- generated by issue-helper. DO NOT REMOVE -->
```

### Feature Request Template

```md
### What problem does this feature solve?

### What does the proposed feature look like?

### Any additional comments? (optional)

<!-- generated by issue-helper. DO NOT REMOVE -->
```

We will develop the form based on the above two templates, and all the above questions will be filled in as a field by the user or contributor in the page we develop.

In addition, we need to support auto-completion and search for related issues that have been created when a user or contributor fills in the issue title. This feature will use [GitHub's search API](https://docs.github.com/en/rest/reference/search#search-issues-and-pull-requests).

For specific page style implementations, we can refer to the following two examples:

- [Vue Issue Helper](https://new-issue.vuejs.org/?repo=vuejs/vue)
- [Ant Design Issue Helper](https://new-issue.ant.design/)

# Drawbacks

Using a web page for users or contributors to fill out the report is simpler and easier than using a complex markdown to fill out as a template. So I see no drawback to this solution.

# Alternatives

N/A

# Adoption strategy

We can use the tool to create a new Issue without modifying the one we have already created.

# Unresolved questions

- Should we allow Issue creation without using this page?

# Future possibilities

In the future, we can also introduce this feature to repositories such as tikv/pd and support more templates.