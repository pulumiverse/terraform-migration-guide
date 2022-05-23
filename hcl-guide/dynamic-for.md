# Dynamic For

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

```typscript
const subnets = [
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
  subnets: [subnets.map(({name, addressPrefix}) => {name, addressPrefix } ],
});
```
