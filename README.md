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
    - geerlingguy.java
    - gsa.datagov-deploy-solr
```


### Variables



## Prerequisites for development

- [Docker](https://www.docker.com/)
- [Python](https://www.python.org/) 2.7 or 3.5+ in a virtualenv


## Development

_Note: when cloning the repo, the directory name must match the role name
defined in the molecule playbooks, e.g. `datagov-deploy-solr`._

    $ git clone https://github.com/GSA/datagov-deploy-solr.git

Install dependencies.

    $ make setup

Run the tests.

    $ make test

To run the tests in debug mode:

    $ molecule --debug test

And you might find it helpful to only run the dependency/playbook step.

    $ molelecule converge

You can log into the machine to inspect it, too.

    $ molecule login

For more about molecule, read the [molecule
docs](https://molecule.readthedocs.io/en/latest/index.html).
