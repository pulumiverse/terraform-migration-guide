# Dynamic Blocks

```terraform
locals {
  standard_tags = {
    Component   = "user-service"
    Environment = "production"
  }
}

resource "aws_autoscaling_group" "example" {
  dynamic "tag" {
    for_each = local.standard_tags

    content {
      key                 = tag.key
      value               = tag.value
      propagate_at_launch = true
    }
  }
}
```


```typescript
const standard_tags = {
  component: "user-service"
  environment: "production"
}

const asg = new aws.autoscaling.Group("asg", {
  tags: standard_tags,
});
```
