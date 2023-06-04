# Dynamic For

Dynamic blocks in Terraform are a way to provide multiple dynamic variations of repeatable blocks, like the subnet example below. This example creates multiple subnets on an Azure Virtual Network, based on our structured variable `subnets`. This example not only requires the use of `dynamic`, but also a `for_each` with a `for` comprehension. This isn't terribly uncommmon with Terraform HCL, but can be rather confusion to the reader.

```terraform
variable "subnets" {
  default = [
    {
      name   = "a"
      number = 1
    },
    {
      name   = "b"
      number = 2
    },
    {
      name   = "c"
      number = 3
    },
  ]
}

locals {
  base_cidr_block = "10.0.0.0/16"
}

resource "azurerm_virtual_network" "example" {
  name                = "example-network"
  resource_group_name = azurerm_resource_group.test.name
  address_space       = [local.base_cidr_block]
  location            = "West US"

  dynamic "subnet" {
    for_each = [for s in subnets: {
      name   = s.name
      prefix = cidrsubnet(local.base_cidr_block, 4, s.number)
    }]

    content {
      name           = subnet.value.name
      address_prefix = subnet.value.prefix
    }
  }
}
```

With Pulumi, we can provide an easier to understand alternative that can be typed and read more easily. The use of `for_each` the inlined comprehensionm, `for`, can be replaced by a `map` function.


```typescript
interface Subnet {
    name: string;
    addressPrefix: number;
}

const subnets: Subnet[] = [
  { name: "a", addressPrefix: 1 },
  { name: "b", addressPrefix: 2 },
  { name: "c", addressPrefix: 3 },
];

const baseCidrBlock = "10.0.0.0/16";

const vn = new azure.network.VirtualNetwork("example", {
  name: "example-network",
  resourceGroupName: resourceGroup.name,
  addressSpaces: [baseCidrBlock],
  location: resourceGroup.location,
  subnets: [
      subnets.map(({name, addressPrefix}) => {name, addressPrefix }
  ],
});
```
