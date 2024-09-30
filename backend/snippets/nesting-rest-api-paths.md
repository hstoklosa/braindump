# Nesting paths in a REST API

## Best Practices

I've tried both design strategies - nested and non-nested endpoints. I've found that:

1. if the nested resource has a primary key and you don't have its parent primary key, the nested structure requires you to get it, even though the system doesn't actually require it.

2. nested endpoints typically require redundant endpoints. In other words, you will more often than not, need the additional /employees endpoint so you can get a list of employees across departments. If you have /employees, what exactly does /companies/departments/employees buy you?

3. nesting endpoints don't evolve as nicely. E.g. you might not need to search for employees now but you might later and if you have a nested structure, you have no choice but to add another endpoint. With a non-nested design, you just add more parameters, which is simpler.

4. sometimes a resource could have multiple types of parents. Resulting in multiple endpoints all returning the same resource.

5. redundant endpoints makes the docs harder to write and also makes the api harder to learn.

In short, the non-nested design seems to allow a more flexible and simpler endpoint schema.

### Reference:

- [What are best practices for REST nested resources?](https://stackoverflow.com/a/36410780/13910414)

## Rule of thumb when nesting resources

Note that this doesn't mean that you should avoid any form of hierarchy in your API. There are cases where it makes sense. As a rule of thumb:

- If the resource makes no sense outside the context of its parent resource, use hierarchy.

- If the resource can live **(1)** alone or **(2)** in a context of parent resources of different types or **(3)** have multiple parents, the hierarchy should not be used.

For instance, lines of a file make no sense outside the context of a file, so:

`GET /file/:fileId`

and:

`GET /file/:fileId/line/:lineIndex`

are fine.

### Reference:

- [Nested REST urls and parent id, which is better design?](https://softwareengineering.stackexchange.com/a/275007)
