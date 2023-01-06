# Root fields and resolvers

GraphQL servers always start with the `Root` or `Query` type.

```javascript
Query: {
  human(obj, args, context, info) {
    return context.db.loadHumanByID(args.id).then(
      userData => new Human(userData)
    )
  }
}
```

* `obj` : This is the last object, which for a field on the root `Query` type is often not used.
* `args` : These are the arguments provided to the field in the GraphQL query.
* `context` : This is a value provided to every resolver and holds essential contextual information, such as the identity of the current user or access to a database.
* `info` : This is a value that holds field-specific information relevant to the current query as well as the schema details.
