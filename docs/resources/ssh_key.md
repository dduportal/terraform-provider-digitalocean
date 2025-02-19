---
page_title: "DigitalOcean: digitalocean_ssh_key"
subcategory: "Account"
---

# digitalocean\_ssh_key

Provides a DigitalOcean SSH key resource to allow you to manage SSH
keys for Droplet access. Keys created with this resource
can be referenced in your Droplet configuration via their ID or
fingerprint.

## Example Usage

```hcl
# Create a new SSH key
resource "digitalocean_ssh_key" "default" {
  name       = "Terraform Example"
  public_key = file("/Users/terraform/.ssh/id_rsa.pub")
}

# Create a new Droplet using the SSH key
resource "digitalocean_droplet" "web" {
  image    = "ubuntu-18-04-x64"
  name     = "web-1"
  region   = "nyc3"
  size     = "s-1vcpu-1gb"
  ssh_keys = [digitalocean_ssh_key.default.fingerprint]
}
```

## Argument Reference

The following arguments are supported:

* `name` - (Required) The name of the SSH key for identification
* `public_key` - (Required) The public key. If this is a file, it
can be read using the file interpolation function

## Attributes Reference

The following attributes are exported:

* `id` - The unique ID of the key
* `name` - The name of the SSH key
* `public_key` - The text of the public key
* `fingerprint` - The fingerprint of the SSH key

## Import

SSH Keys can be imported using the `ssh key id`, e.g.

```
terraform import digitalocean_ssh_key.mykey 263654
```
