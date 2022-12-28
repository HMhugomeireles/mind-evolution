# Labeled Tuple Elements

This is purely for documentation purposes, it has no semantics. They are just a way of putting names in the type signature--they type check identically to tuples without names, and the runtime behavior is identical as well.

A tuple is a typed array with a pre-defined type and length this help give types and names to each index of the Array and define the length of the Array.

```typescript
// Before
type Range = Array<number>
const arrayExample = [...];
// In this you have called each index the name that you want 
const [index1, index2] = arrayExample;

// With Tuple

// Range type, have position name [start, end]:
type Range = [start: number, end: number];

// you could use unnamed tuples:
type Range = [number, number];
```
