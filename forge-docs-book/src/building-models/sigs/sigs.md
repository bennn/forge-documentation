# Sigs

```admonish danger title="TODO"
- Link to integers in Forge at hyperlink
- Do sigs have to be defined before they are used?
```

_Sigs_ are the basic building block of any model in Forge. Sigs represent the "things" of the system we are modeling. You can think of a `sig` as analogous to a class in an object-oriented programming language. You can declare a `sig` in the following way:

```
sig <name> {}
```

A `sig` can also have one or more _fields_, which define relationships between that `sig` and other `sig`s and types.

```
sig <name> {
    <field>,
    <field>,
    ...
    <field>
}
```

```admonish note title="Syntax Note"
Ensure that there is a **comma after every field except for the last one**. This is a common source of compilation errors when first defining a model!
```

## Fields

Fields allow us to define relationships between Sigs and other "things" in our model (including other Sigs). Each _field_ in a `sig` has:

- a _**name**_;
- a [_**multiplicity**_](multiplicity.md) (`set`, `one`, `lone`, `pfunc`, or `func`);
- a [_**type**_](sig-types.md)_**.**_

Put together, a field takes the form:

```
name: multiplicity type
```

<!-- - The **name** of a field does exactly what it sounds like, and assigns a name to the relationship. You can use the name of the relationship to reference the relationship when writing the "rules" of the system (we'll cover this when we talk about [constraints](../constraints/constraints.md)).
- The **multiplicity** of a field allows you to define the type of relationship -->

```admonish example title="Example: Sig w/ One Field"
**Basic Sig with Fields (Linked List):**

A model of a circularly-linked list might have a `sig` called `Node`. `Node` might then have a field `next: one Node` to represent the contents of every `Node`'s `next` reference. We use `one` here since every `Node` has exactly one successor.&#x20;

~~~
sig Node {
    next: one Node
}
~~~
```

```admonish example title="Example: Sig w/ Multiple Fields"
**Basic Sig with Fields (Binary Tree):**

A model of a binary tree might have a `sig` called `Node`. `Node` might then have three fields:

- `left: lone Node` and `right: lone Node` to represent the `Node`'s children. We use `lone` here since the left/right child can either be empty, or contain exactly one `Node`.
- `val: one Int` to represent the value of each Node, where we have decided that every `Node` should have an Integer value. We use `one` here because each `Node` should have exactly one Integer as its value.

~~~
sig Node {
    left: lone Node,
    right: lone Node,
    val: one Int
}
~~~
_**(`Int`** is a type provided by Forge. Read more about [valid types](./sig-types.md), and [Integers in Forge]())._
```

<!-- ```admonish note title="Int?"
**`Int`** is a type provided by Forge. Read more about [valid types](sigs.md#types), and [Integers in Forge](../integers.md).
``` -->

```admonish example title="Example: Sig w/ No Fields"

#### Example - Basic Sig without Fields:

Not every `sig` in a model needs to have fields to be a useful part of the model! `sig`s with no fields are often used in conjunction with other `sig`s that reference no-field `sig`s.

One such example might look like this:

~~~
sig Student {}
sig Group {
    member: set Student
}
~~~
```
