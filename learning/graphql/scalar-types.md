# Scalar types

These are similar to primitive types in any programming language and this will always resolve to concrete data.

Graphql comes with the following scalar types:

* **Int** is a signed 32-bit integer.
* **Float** is a signed double-precision floating point value.
* **String** is a UTF-8 character sequence.
* **Boolean** is either true or false.
* **ID** represents a unique identifier, which is often used either as a way to fetch an object or as the key for a cache. The ID type is serialized in the same way as a String. However, defining it as an ID signifies that it’s not intended to be readable for humans.

```

  type Pizza {
    id: ID!
    pizza: String!
    stock: Int!
    toppings: [Topping!]!
  }
```

we have this graphql type, the object type should convert automatically.

The scalar types give us the possibility to create other custom types.

```typescript
// Some Example

import { ApolloServer } from '@apollo/server';
import { startStandaloneServer } from '@apollo/server/standalone';
import { GraphQLScalarType, Kind, GraphQLError } from 'graphql';

// Basic schema
const typeDefs = `#graphql
  scalar Odd

  type Query {
    # Echoes the provided odd integer
    echoOdd(odd: Odd!): Odd!
  }
`;

// Validation function for checking "oddness"
function oddValue(value: number) {
  if (typeof value === 'number' && Number.isInteger(value) && value % 2 !== 0) {
    return value;
  }
  throw new GraphQLError('Provided value is not an odd integer', {
    extensions: { code: 'BAD_USER_INPUT' },
  });
}

const resolvers = {
  Odd: new GraphQLScalarType({
    name: 'Odd',
    description: 'Odd custom scalar type',
    parseValue: oddValue,
    serialize: oddValue,
    parseLiteral(ast) {
      if (ast.kind === Kind.INT) {
        return oddValue(parseInt(ast.value, 10));
      }
      throw new GraphQLError('Provided value is not an odd integer', {
        extensions: { code: 'BAD_USER_INPUT' },
      });
    },
  }),
  Query: {
    echoOdd(_, { odd }) {
      return odd;
    },
  },
};

const server = new ApolloServer({
  typeDefs,
  resolvers,
});

const { url } = await startStandaloneServer(server);

console.log(`🚀 Server listening at: ${url}`);
```
