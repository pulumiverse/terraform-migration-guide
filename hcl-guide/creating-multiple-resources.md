# Creating Multiple Resources

Creating multiple resources is a rather common operation with cloud infrastrucre and HCL provides a `count` option that allows you to specify that you want some arbitrary number.

```hcl
resource "null_resource" "simple" {
  count = 2
}
```

When switching to Pulumi, you can use the loop constructs within the supported programming languages; which also allows your developers to adopt an idiom that reflects the way your organisation writes code: such as imperative or functional.

```typescript
// 1. Imperative
for (let i = 0; i < 10; i++) {
  let resource = i;
}

// 2. Functional Approach
let fResources = new Array(10).fill(true).map((_e, i) => i);
```

The imperative loop is immediately familiar to many developers and while the functional approach is rather contrived, it does bring with it the ability to write code that is more testable.
