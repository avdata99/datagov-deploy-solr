[![CircleCI](https://circleci.com/gh/GSA/datagov-deploy-solr.svg?style=svg)](https://circleci.com/gh/GSA/datagov-deploy-solr)

# datagov-deploy-solr

This project is part of [datagov-deploy](https://github.com/GSA/datagov-deploy).

Ansible role to deploy solr.


## Usage

Include this role in your `requirements.yml`.

```yaml
- src: https://github.com/gsa/datagov-deploy-solr.git
```

The role depends on having Java installed. We recommend including the role
`geerlingguy.java` on your solr hosts.

Example playbook:

```yaml
---
- name: Solr
  hosts: solr
  roles:
    - role: geerlingguy.java
      java_packages:
        - openjdk-8-jdk
    - role: gsa.datagov-deploy-solr
```

_Note: for trusty, use `openjdk-7-jdk`._


### Variables

See [geerlingguy.solr](https://github.com/geerlingguy/ansible-role-solr/blob/4.3.0/README.md) for
additional variables.

**`solr_cores`** arary[string] (required)

The solr cores to create. This should be either `inventory` or `catalog`, or
both. The solr config should be created in this role.

**`solr_home`** string

The directory to use for solr's data files.

**`solr_port`** string

The port number for solr to listen.

**`is_solr_replica`** boolean

Configures the host as a Solr replica.

**`solr_master_server`** string

IP or hostname of the Solr master this replica should replicate from.


## Prerequisites for development

- [Docker](https://www.docker.com/)
- [Python](https://www.python.org/) 3.6
- [Pipenv](https://pipenv.readthedocs.io/en/latest/)


## Development

_Note: when cloning the repo, the directory name must match the role name
defined in the molecule playbooks, e.g. `datagov-deploy-solr`._

    $ git clone https://github.com/GSA/datagov-deploy-solr.git

Install dependencies.

    $ make setup

Run the tests.

    $ make test

To run the tests in debug mode:

    $ pipenv run molecule --debug test

And you might find it helpful to only run the dependency/playbook step.

    $ pipenv run molecule converge

You can pass arguments to ansible-playbook in order to pickup at a specific
step.

    $ pipenv run molecule converge -- --start-at-task='datagov-deploy-solr : copy solr schema file'

You can log into the machine to inspect it, too.

    $ pipenv run molecule login

For more about molecule, read the [molecule
docs](https://molecule.readthedocs.io/en/latest/index.html). For quick tips about
developing with molecule, see our
[wiki](https://github.com/GSA/datagov-deploy/wiki/Developing-Ansible-roles-with-Molecule).
