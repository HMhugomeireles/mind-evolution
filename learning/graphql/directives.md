# Directives

Directives are Decorates from graphql schema which allows us to create behavior about the field and by default, graphql gives us 3 decorates we can use.

* **@deprecated(reason: String)** - mark a schema or field the property are deprecated and you can give an explication about the field deprecation.
* **@skip(if: Boolean)** - the decorated gives us the possibility to tell the graphql server to ignore the field base on the evaluation that the expression in the case is true the server will ignore the field.
* **@inclue(if: Boolean)** - this decorated is almost the same as the _@skip_ but only ignores if the evaluation of the expression is false.&#x20;

The Apollo server does not provide built-in support for custom directives that transform a schema, for we create customer directives is recommended to use the @graphql-tools library.&#x20;

Disclaimer about custom directives. They can be used with graph federation.
