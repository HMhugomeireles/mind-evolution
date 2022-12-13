# Fragments

What are Fragments in a query?

In graphql, we can create queries and give an alias to that queries and the fields we want to receive and that is where the fragments came to play. With it you can reduce code repetition and reuse in all queries we create with the spread operation

```graphql

query GetPizzas {
  Neapolitan: pizzas(pizza: "Neapolitan Pizza") {
    ...pizzaFields
  }
  Chicago: pizzas(pizza: "Chicago Pizza") {
    ...pizzaFields
  }
}

fragment pizzaFields on Pizza {
    id
    pizza
}

```

In this case, we create a fragment that will contain all fields that can be used in both query

> A fragment can’t refer to itself since this could cause an unbounded result. This will cause Internal server error, with message "Maximun call stack size exceeded".
