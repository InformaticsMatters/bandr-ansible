# bandr-ansible

![lint](https://github.com/InformaticsMatters/bandr-ansible/workflows/lint/badge.svg)

![GitHub tag (latest SemVer)](https://img.shields.io/github/v/tag/informaticsmatters/bandr-ansible)

[![CodeFactor](https://www.codefactor.io/repository/github/informaticsmatters/bandr-ansible/badge)](https://www.codefactor.io/repository/github/informaticsmatters/bandr-ansible)

AWX-compatible Ansible playbooks for the deployment of our backup and recovery
([bandr]) container images as **CronJobs** (for Backup) and **Jobs**
(for Recovery) to an existing **Namespace**.

The playbooks assume a **ServiceAccount** exists in the namespace.

## Testing
To test this repository (Normally done via GitHib Actions)
we essentially employ yaml and ansible lint code. From a suitable
environment...

    $ python -m venv ~/.venv/bandr-ansible
    $ source ~/.venv/bandr-ansible/bin/activate
    $ pip install --upgrade pip
    $ pip install -r requirements.txt
    $ pip install -r build-requirements.txt

Run the following: -

    $ yamllint .
    $ find . -type f -name '*.yaml.j2' -exec yamllint {} +
    $ ansible-lint

---

[bandr]: https://github.com/InformaticsMatters/bandr
