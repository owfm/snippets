Often it is useful to use the Boolean constructor as a callback to the filter array method, to remove any falsy values from the array:

```typescript
console.log([1, 2, undefined, undefined, 3, 4].filter(Boolean)); // [1,2,3,4]
```

However, if you have an array that is typed as, for example, `type NullableArr = (number | undefined)[]` and try the same thing:

```typescript
const a: NullableArr = [1, 2, undefined, undefined, 3, 4];
const b = a.filter(Boolean);
```

Even though `b` is known to be of type `number[]`, Typescript is unaware of this so thinks it can still contain undefined values.

We can create a replacement callback instead of `Boolean` which is TS aware.

```typescript
type Truthy<T> = T extends false | "" | 0 | null | undefined ? never : T;

export function truthy<T>(value: T): value is Truthy<T> {
  return !!value;
}
```

This can be used in the same way as the `Boolean` filter above
