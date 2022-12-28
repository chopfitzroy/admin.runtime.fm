# Coffee and code API setup ☕

Ansible scripts to automate API setup, largely based on [this guide](https://www.digitalocean.com/community/tutorials/how-to-use-ansible-to-automate-initial-server-setup-on-ubuntu-22-04).

PocketBase specific setup largely based on [this guide](https://github.com/pocketbase/pocketbase/discussions/512).

### Gettings started 🚀

The below guide assumes you are using [Digital Ocean](https://www.digitalocean.com/) but a lot of the code here should work with any cloud provider.

#### Create virtual machine 💧

Create a new Droplet on Digital Ocean (Debian was used when creating this guide but Ubuntu should work as well).

When creating the Droplet it is recommend you also create a volume of 20GB or larger.

#### Edit your hosts 📝

Edit your `/etc/ansible/hosts` on your local machine to include:

```sh
[servers]
cac_api ansible_host={{ droplet_ip }}
```

#### Run the playbook 📚

```sh
ansible-playbook main.yml
```

#### Propagation delays 🛑

During intial deployment there were delays between deploying the site and the SSL certificates being correctly registered.

When deploying allowing up to 24 hours for certificates to be registered.

### Reasoning 🤔

Why Ansible? It runs everywhere and is fairly simple to port over to other operating systems when required.

### Future improvements 🔮

- [ ] Handle local setup additional to remote setup
