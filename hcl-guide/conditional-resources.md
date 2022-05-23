# Conditional Resources

With HCL, you can define resources that are conditionally created based on the value of a variable and using this in a ternary statement to set the `count` value to `0` or `1`.

An example of such looks like this:

```hcl
variable "enabled" {
  type        = bool
  default     = true
}

resource "null_resource" "simple" {
count = (var.enabled ? 1 : 0)
}
```

This works well most of the time, though the legibility of the code is certainly questionable.

In Pulumi, we can write these conditions in a much more comprehensible way. Let's take a look at the same example, but with Pulumi's TypeScript SDK:

```typescript
const createThisResource = true;

if(createThisResource) {
  let resource = 1;
}
```

You can use the natural branching constructs of all our supported languages to provide an interface to your infrastructure that just isn't possible with HCL.
