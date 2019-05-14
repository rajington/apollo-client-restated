# apollo-link-stateful
Add common functionality to Apollo [`local-state`](https://www.apollographql.com/docs/react/essentials/local-state) via clientside [schema directives](https://www.apollographql.com/docs/graphql-tools/schema-directives).

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
  page: Int! @stateful(default: 1, actions: [INCREMENT, DECREMENT])
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
  visible: Boolean! @stateful(default: false, actions: [TOGGLE])
}

# GENERATED
type Mutation {
  visibleToggle
}
```

### `set`
```gql
type Query {
  name: String @stateful(actions: [SET])
}

# GENERATED
type Mutation {
  nameSet(name: String)
}
```

### custom actions
```gql
type Query {
  sign: String @stateful(actions: [INVERT])
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
