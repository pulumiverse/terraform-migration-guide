# Data Lookups

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
