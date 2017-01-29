# terraform

Terraform is truly awesome infrastructure as code from Hashicorp. Here are some scattered notes.

## Modules

A good example of how to go from non-modular to modular code:

https://github.com/dwmkerr/terraform-consul-cluster/pull/4

## AMI Images

A common requirement is to be able to get a specific AMI, but as they are per region and change over time, this can often feel a little clunky. Here's a nice trick:

```terraform

data "aws_ami" "amazonlinux" {
  most_recent = true

  owners = ["137112412989"]

  filter {
    name   = "architecture"
    values = ["x86_64"]
  }

  filter {
    name   = "root-device-type"
    values = ["ebs"]
  }

  filter {
    name   = "virtualization-type"
    values = ["hvm"]
  }

  filter {
    name   = "name"
    values = ["amzn-ami-hvm-*"]
  }
}
```

See https://www.terraform.io/docs/providers/aws/d/ami.html for info on this trick.
