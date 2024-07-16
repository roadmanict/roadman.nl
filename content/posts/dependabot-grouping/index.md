+++
title = 'Dependabot Grouping'
date = 2024-07-16T14:20:51+02:00
draft = true

tags = ['Angular', 'NodeJS', 'Typescript', 'NPM', 'Dependabot']
+++

# Dependabot grouping

For certain dependencies like Angular it can be useful to group Dependabot Pull Requests. This can be done by using the grouping feature:

```yaml
version: 2
updates:
  - package-ecosystem: "github-actions"
    schedule:
      interval: "weekly"
    directory: "/"
    commit-message:
      prefix: "deps"
    open-pull-requests-limit: 10
  - package-ecosystem: "npm"
    directory: "/"
    schedule:
      interval: "daily"
    commit-message:
      prefix: "deps"
    open-pull-requests-limit: 10
    target-branch: "main"
    rebase-strategy: "auto"
    groups:
      angular:
        applies-to: version-updates
        patterns:
          - "@angular*"
        update-types:
          - "minor"
          - "patch"
```

In the above example I configured a `Angular` group. Matching all dependencies that start with `@angular` by applying a `@angular*` pattern. The Angular dependencies will only be grouped when minor or patch versions change. If there will be a new major angular version, a separate Dependabot pull request will be created.
