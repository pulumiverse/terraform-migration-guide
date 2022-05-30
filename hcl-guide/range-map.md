# Range Map

When you wish to create multiple resources that are very similiar, you can use the `for_each` argument to create them all with a single resource definition. There are some constraints with Terraform HCL, such as not being able to use `for_each` along with `count`. The use of `toset` also ensures that we don't attempt to create a duplicate resource with the same name.

```terraform
locals {
  letters = ["A", "B", "C"]
}

resource "null_resource" "letters" {
  for_each = toset(local.letters)
}
```

Terraform HCL and TypeScript aren't terribly disimiliar here, only by using the `forEach` prototype function on our Array/Set object, we can actually include more custom code or create more than one resource per iteration - allowing us to remove some boiler plate that would require us to drop down to a Terraform module with Terraform HCL.

```typescript
const letters = new Set(["A", "B", "C"]);
letters.forEach(letter => new Resource(letter, { ... }));
```
