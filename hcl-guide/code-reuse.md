# Code Reuse

With Terraform, the way that we reuse code is through the use of Terraform modules.

Modules are directories, or often Git repositories, that contain `tf` files with HCL.

Parameters can be passed to these modules via variables.

Using a Terraform module looks like:

```terraform
module "servers" {
  source = "./app-cluster"

  servers = 5
}
```

Here, we're using a module that lives in the `app-cluster` directory and passing in the value of `5` to the `servers` variable.

Modules work well in Terraform, but they're not as flexible as code re-use in Pulumi. Passing configuration to a module is done via a flat list of variables within the module declaration and can become rather difficult to maintain as the list gets bigger; especially when you venture into the land of nested modules.

With Pulumi, we structure our programs based on the programming language we decide to use. This means if we're using TypeScript, we can build an interface (or even a class) that we can use to pass configuration throughout our program; giving us strict type verification. This isn't restricted to TypeScript, and works with all our supported languages.

Code re-use within Pulumi works with the native package managers for each programming language too; meaning that you'd use:

- Go modules with Go
- npm with JavaScript and TypeScript
- PyPi with Python
- Maven with Java
- nuget for dotNet

These package managers are all ready extremely familiar to most developers, making reusing and sharing code across Pulumi programs a breeze.
