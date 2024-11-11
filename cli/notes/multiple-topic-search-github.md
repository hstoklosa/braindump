# Search for multiple topics using GitHub CLI

With [GitHub CLI](https://cli.github.com/), it can be done like this:

```bash
gh search repos --topic ecs --topic go
```

or if you want JSON and/or additional fields:

```bash
gh search repos --topic ecs --topic go --json url,description,stargazersCount,createdAt,updatedAt
```

`AND` is implied with multiple `--topic` parameters and the default sort order is the number of stars.
