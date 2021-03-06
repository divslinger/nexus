```ts
objectType(typeName: string, fn: ObjectDefinitionBlock): NexusObjectType
```

The most basic components of a GraphQL schema are object types, a type you can fetch from your schema, with fields:

```ts
const User = objectType({
  name: 'User',
  definition(t) {
    t.int('id', { description: 'Id of the user' })
    t.string('fullName', { description: 'Full name of the user' })
    t.field('status', { type: 'StatusEnum' })
    t.list.field('posts', {
      type: Post, // or "Post"
      resolve(root, args, ctx) {
        return ctx.getUser(root.id).posts()
      },
    })
  },
})

const Post = objectType({
  name: 'Post',
  definition(t) {
    t.int('id')
    t.string('title')
  },
})

const StatusEnum = enumType({
  name: 'StatusEnum',
  members: {
    ACTIVE: 1,
    DISABLED: 2,
  },
})
```

`queryType` / `mutationType` are shorthand for the root types.

Check the type-definitions or [the examples](https://github.com/graphql-nexus/nexus/tree/develop/examples) for a full illustration of the various options of `objectType`, or feel free to open a PR on the docs to help document!
