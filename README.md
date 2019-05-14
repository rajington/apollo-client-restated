# apollo-link-stateful
Add common functionality to [`apollo-link-state`](https://www.apollographql.com/docs/link/links/state) via clientside [schema directives](https://www.apollographql.com/docs/graphql-tools/schema-directives).

## Install

```js
import stateful from 'apollo-link-stateful'

const schema = makeExecutableSchema({
  typeDefs,
  schemaDirectives: {
    stateful,
  }
})
```

## Examples

### `increment`/`decrement`
```gql
type Query {
  page: Int! @stateful(default: 1, actions: ["increment", "decrement"])
}

# GENERATED
type Mutation {
  pageIncrement
  pageDecrement
}
```

### `toggle`
```gql
type Query {
  visible: Boolean! @stateful(default: false, actions: ["toggle"])
}

# GENERATED
type Mutation {
  visibleToggle
}
```

### `set`
```gql
type Query {
  name: String @stateful(actions: ["set"])
}

# GENERATED
type Mutation {
  nameSet(name: String)
}
```

### custom actions
```gql
type Query {
  sign: String @stateful(actions: ["invert"])
}

# GENERATED
type Mutation {
  signInvert
}
```

```js
const schema = makeExecutableSchema({
  typeDefs,
  schemaDirectives: {
    stateful({
      invert: sign => -sign,
    }),
  }
})
```
