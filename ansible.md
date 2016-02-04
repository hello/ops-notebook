## Ansible

Not every app can be easily deployed by sanders.
For the few snowflakes, we should use ansible.

## Currently supported

The only server that is currently entirely configured with ansible is the store-db-proxy server.
This server acts as a proxy between VPC-enabled and EC2 classic environments.

Please refer to the [github repo](https://github.com/hello/ansible) for more details.


## Transition plan

- [ ] Base AMI creation
- [ ] Bastion Host setup
- [ ] Migrator environment
- [ ] Research environment
- [ ] Dev environment