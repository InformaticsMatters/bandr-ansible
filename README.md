# bandr-ansible

![lint](https://github.com/InformaticsMatters/bandr-ansible/workflows/lint/badge.svg)

![GitHub tag (latest SemVer)](https://img.shields.io/github/v/tag/informaticsmatters/bandr-ansible)

[![CodeFactor](https://www.codefactor.io/repository/github/informaticsmatters/bandr-ansible/badge)](https://www.codefactor.io/repository/github/informaticsmatters/bandr-ansible)

AWX-compatible Ansible playbooks for the deployment of our backup and recovery
([bandr]) container images as **CronJobs** (for Backup) and **Jobs**
(for Recovery) to an existing **Namespace**.

There are two roles, `backup` and `recovery` and the playbooks assume
a suitable **ServiceAccount** exists in the corresponding  **Namespace**.

>   Refer to the [bandr] repository where you wil find ample documentation in the
    corresponding `backup.py` and `recovery.py` modules relating to how the backup and
    recovery containers work and how they are configured.

## Installing a backup
If you have a Postgres database in a Kubernetes **Namespace** you can simplify the
deployment of a backup strategy using the `site-backup.yaml` playbook.

As with most of our Python repositories, create an environment and install the
relevant packages, and set your `KUBECONFIG` to an appropriate file for a cluster: -

    python -m venv venv
    source venv/bin/activate
    pip install --upgrade pip
    pip install -r requirements.txt

    export KUBECONFIG=~/k8s-configs/config-local

**A comprehensive example**

In this example let's setup a comprehensive backup strategy that backs up a
postgres database every 4 hours, keeping daily backups for a week, weekly backups for a
month and monthly backups for 2 years. This will result in a total of 38 backup files
(6 hourly + 6 daily + 3 weekly + 23 monthly).

Copy `parameters-template.yaml` and create a `parameters.yaml` file
(this new file will be ignored from any git commit).

Assuming your database has a **Service** called `database`, and your admin user is
`postgres`, then the template variables are already setup to provide you with 2 
year's worth of backups as described; you just need to provide: -

- The **Namespace**
- The **ServiceAccount**
- The postgres administrator's password
- The backup volume size

With this done, run the playbook: -

    ansible-playbook -e @parameters.yaml site-backup.yaml

This example will install four **CronJob** objects.
 
## Testing
To test this repository (Normally done via GitHib Actions)
we essentially employ yaml and ansible lint code. From a suitable
environment...

    python -m venv ~/.venv/bandr-ansible
    source ~/.venv/bandr-ansible/bin/activate
    pip install --upgrade pip
    pip install -r requirements.txt
    pip install -r build-requirements.txt

Run the following: -

    yamllint .
    find . -type f -name '*.yaml.j2' -exec yamllint {} +
    ansible-lint

---

[bandr]: https://github.com/InformaticsMatters/bandr
