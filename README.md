# GraphQL Symmetric Input Types

Have you ever had an endpoint take the same nested type as an input as it spit out and you were anoyed by having to write the same types as input types again? Then this is the tool for you!

## Setup

First run `npm install --save graphql-symmetric-input-types`

```js
import transformInputTypes from "graphql-symmetric-input-types";

const typeDefs = `
  type Car {
    id: ID!
    name: String
    brand: String
  }

  type Query {
    car(
      id: ID!
    ): Car
  }
  type Mutation {
    addCar(id: Car!): Car
  }
  `;

const correctTypeDefs = `
  type Car {
    id: ID!
    name: String
    brand: String
  }

  input type CarInput {
    id: ID!
    name: String
    brand: String
  }

  type Query {
    car(
      id: ID!
    ): Car
  }
  type Mutation {
    addCar(id: CarInput!): Car
  }
  `;

// correctTypeDefs === typeDefsWithInputTypes
const typeDefsWithInputTypes = transformInputTypes(typeDefs);
```

## License

MIT
