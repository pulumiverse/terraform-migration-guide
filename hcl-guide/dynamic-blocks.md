# Dynamic Blocks

Dynamic blocks in Terraform provider a way to produce multiple, repeatable, blocks of Terraform HCL with some dynamic value to iterate over. In the example below, we're adding multiple tags to the AutoScaling Group based on a local variable, called `standard_tags`.

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

Terraform HCL's dynamic blocks certainly seem confusing to people that haven't used them before and as such Pulumi's use of primitive programming constructs, such as maps, arrays, and loops, is immediately familiar on first glance.

```typescript
const standard_tags = {
  component: "user-service"
  environment: "production"
}

const asg = new aws.autoscaling.Group("asg", {
  tags: standard_tags,
});
```
