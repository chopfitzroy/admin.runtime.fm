# Runtime FM API setup ☕

Ansible scripts to automate API setup, largely based on [this guide](https://www.digitalocean.com/community/tutorials/how-to-use-ansible-to-automate-initial-server-setup-on-ubuntu-22-04).

PocketBase specific setup largely based on [this guide](https://github.com/pocketbase/pocketbase/discussions/512).

Litestream specific setup largely based on [this guide](https://litestream.io/guides/systemd/).

### Gettings started 🚀

The below guide assumes you are using [Digital Ocean](https://www.digitalocean.com/) but a lot of the code here should work with any cloud provider.

#### Create virtual machine 💧

Create a new Droplet on Digital Ocean (Debian was used when creating this guide but Ubuntu should work as well).

#### Create volume 📦

Once you have created your Droplet you have the option of creating a volume to attach to the droplet 20GB should be sufficient.

**NOTE:** Ansible looks for the first available mounted volume, if you attach more than one volume you may need to tweak the playbook.

#### Create your spaces 🌌

Additionally you can also make use of Digitial Ocean spaces (or any S3 compatiable storage) for handling file uploads and database backups.

We recommend two buckets one for [direct use with PocketBase](https://pocketbase.io/docs/files-handling/#storage-options) and one for use with [Litestream](https://litestream.io/).

#### Edit your hosts 📝

Edit your `/etc/ansible/hosts` on your local machine to include:

```sh
[servers]
cac_api ansible_host={{ droplet_ip }}
```

#### Add your spaces credentials 🗝

Add your Digital Ocean spaces credentials to `vars/generic.yml` to configure Litestream backups.

If you don't want to use Litestream you can bypass the setup using the following command:

```sh
ansible-playbook main.yml --tags "pocketbase"
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
