# Data Lookups

Data lookups allow us to fetch values from existing, potentially non-managed, resources from our various providers. Doing this with Terraform HCL and Pulumi is relatively trivial in both.

```terraform
data "kubernetes_service" "example" {
  metadata {
    name = "service-name"
  }
}
```

```typescript
const svc = k8s.core.v1.Service.get("example", "service-name");
```
