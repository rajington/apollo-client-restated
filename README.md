> This project practices [README-driven development](https://tom.preston-werner.com/2010/08/23/readme-driven-development.html)

# apollo-client-restated
Add common functionality to [Apollo local state](https://www.apollographql.com/docs/react/essentials/local-state) via clientside [schema directives](https://www.apollographql.com/docs/graphql-tools/schema-directives).

## Install

```js
import restated from 'apollo-client-restated'

const schema = makeExecutableSchema({
  typeDefs,
  schemaDirectives: {
    restated,
  }
})
```

## Examples

### `increment`/`decrement`
```gql
type Query {
  page: Int! @restated(default: 1, actions: [INCREMENT, DECREMENT])
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
  visible: Boolean! @restated(default: false, actions: [TOGGLE])
}

# GENERATED
type Mutation {
  visibleToggle
}
```

### `set`
```gql
type Query {
  name: String @restated(actions: [SET])
}

# GENERATED
type Mutation {
  nameSet(name: String)
}
```

### custom actions
```gql
type Query {
  sign: String @restated(actions: [INVERT])
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
    restated({
      invert: sign => -sign,
    }),
  }
})
```
