# Contributing

New roles, playbooks, and modules are always welcome.

Contributions must meet a minimum criteria:

* Must have a Molecule scenario/test
* Must be idempotent
* Must pass Ansible linter (run `./runLint.sh` script)

**Table of Content:**

* [Prerequisites](#prerequisites)
* [Creating a new role](#creating-a-new-role)
* [Creating a new playbook](#creating-a-new-playbook)
* [Creating a new collection](#creating-a-new-collection)

## Prerequisites

* `git`
* Docker CE
* Python >= 3.6
  * Creating a Python `venv` is highly recommended!
* Python modules listed in `ci-requirements.txt`
  * Can be installed using `pip install -r ci-requirements.txt`
* Repository cloned to `.../ansible_collections/<collection_namespace>/<collection_name>`

**Note:** The clone path is _extremely_ important for the development environment.
`collection_namespace` and `collection_name` may be retrieved from the `galaxy.yml` file.

## Creating a new role

The role must have a minimum of
* `README.md` file describing its functionality and requirements
* `meta/main.yml` file with the authorship and license information for Ansible Galaxy
* `tasks/main.yml` file with the tasks

This structure can be generated from the provided skeleton structure using

```
ansible-galaxy role init --init-path ./roles --role-skeleton ./skeleton_role awesome_role
```

**Note:** Role names are limited to contain only lowercase alphanumeric characters, plus `_` and must begin with a letter.

### Molecule Tests

To meet the acceptance requirements, the role must have a reasonable Molecule scenario defined.

In the `molecule/` directory, copy the `default` scenario, and update the `converge.yml` and `verify.yml` playbooks to run/check your new role

These playbooks may be run using the `molecule [converge|verify] -s scenario_name` command, similar to Chef's Test-Kitchen framework

## Creating a new collection

Creating a new collection is quite simple:

* Create a new repository from `Coming Soon!`
* Update the `README.md` and `galaxy.yml` files to match your desired namespace and collection name

To enable the Travis, set the following variables:

* `GITHUB_OAUTH_TOKEN` - GitHub Personal Access Token for tagging/publishing release
* `ARTIFACTORY_TOKEN` - Artifactory API Token, if required for your roles/playbooks
* `ARTIFACTORY_URL` - Artifactory URL, if required for your roles/playbooks
* `ARTIFACTORY_REPO` - Artifactory REPO, if required for your roles/playbooks

**Note:** Make sure to _never_ commit any sensitive or private data!
