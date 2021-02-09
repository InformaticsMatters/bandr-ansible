# bandr-ansible

![lint](https://github.com/InformaticsMatters/bandr-ansible/workflows/lint/badge.svg)

![GitHub tag (latest SemVer)](https://img.shields.io/github/v/tag/informaticsmatters/bandr-ansible)

[![CodeFactor](https://www.codefactor.io/repository/github/informaticsmatters/bandr-ansible/badge)](https://www.codefactor.io/repository/github/informaticsmatters/bandr-ansible)

AWX-compatible Ansible playbooks for the deployment of our backup and recovery
([bandr]) container images as **CronJobs** (for Backup) and **Jobs**
(for Recovery) to an existing **Namespace**.

The playbooks assume a **ServiceAccount** exists in the namespace.

---

[bandr]: https://github.com/InformaticsMatters/bandr
