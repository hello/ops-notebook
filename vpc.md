## VPC + Subnets


Our main VPC (`vpc-prod vpc-961464f3`) has several public and private subnets at the moment.

### Original setup
Original subnets:

- `subnet-28c6565f` `1A`
- `subnet-28c6565f` `1B`

Both subnets are public, which means all instances launched into the subnets are publicly accessible. They use a shared internet gateway to access the internet.



### New setup
New subnets:

- `subnet-838a3bf5` `Pub1A`
- `subnet-c68233b0` `Priv1A`
- `subnet-8abb70d2` `Pub1B`
- `subnet-a4bb70fc` `Priv1B`


There is now a managed NAT gateway running in `Pub1A`. It allows instances in `Priv1A` to access the internet through an internet gateway.
The NAT gateway has been assigned an EIP (`52.3.92.74`) which **should never be changed**.

We will eventually have a NAT gateway in each AZ, for HA purposes.
Right now, `Pub1B` and `Priv1B` are not being used.



### Transition

We will eventually transition all our instances into these new subnets.
Tentative transition plan as follows:

- [ ] Enable HA NAT for `Priv1B` in `Pub1B`
- [ ] Create prod bastion host
- [ ] Migrate workers to run into `Priv1A` **and** `Priv1B`
- [ ] Migrate firehose to run into `Priv1A` **or** `Priv1B`
- [ ] Migrate admin to run into `Priv1A` **or** `Priv1B`
- [ ] Migrate app to run into `Priv1A` **and** `Priv1B`
- [ ] Migrate service to run into `Priv1A` **and** `Priv1B`
- [ ] Retire `1A` and `1B` subnets.


### Naming/Network conventions

Subnets name should identify their accessibility `Pub|Priv` and the AZ in which they are running `1A|1B|1X`.
Current CIDR blocks are defined as follows:

- `subnet-28c6565f` `1A` `10.0.0.0/24` 
- `subnet-28c6565f` `1B` `10.0.1.0/24`

- `subnet-838a3bf5` `Pub1A`  `10.0.3.0/24`
- `subnet-c68233b0` `Priv1A` `10.0.2.0/24`
- `subnet-8abb70d2` `Pub1B`  `10.0.5.0/24`
- `subnet-a4bb70fc` `Priv1B` `10.0.4.0/24`


Odd CIDR for public subnets. Example: `10.0.3.X/X` and `10.0.5.X/X`
Even CIDR for private subnets. Example: `10.0.2.X/X` and `10.0.4.X/X`

Exceptions: original subnets have odd and even CIDR blocks and are both public.


