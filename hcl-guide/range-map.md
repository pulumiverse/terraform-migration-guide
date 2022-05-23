# Range Map

```terraform
// forEach Example
locals {
  letters = ["A", "B", "C"]
}

resource "null_resource" "letters" {
  for_each = toset(local.letters)

  triggers = {
    name = each.value
  }
}
```


```typescript
const letters = ["A", "B", "C"];
letters.forEach(letter => new Resource(letter, { ... }));
```
