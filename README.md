# Metabase application stack for Kubernetes on Wodby

Deploy Metabase, the open source business intelligence tool, on Kubernetes
with Wodby.

This repository defines the Wodby stack manifest and its default service
composition.

<!-- wodby:generated:start -->

## Stack contract

- [Metabase stack on Wodby](https://wodby.com/stacks/metabase)
- [Browse Wodby application stacks](https://wodby.com/stacks)
- [Wodby stack documentation](https://wodby.com/docs/2.0/stacks/)
- [Stack manifest reference](https://wodby.com/docs/2.0/stacks/template/)

## Service definitions

- [Metabase service](https://github.com/wodby/service-metabase)
- [PostgreSQL service](https://github.com/wodby/service-postgres)
- [OpenSMTPD service](https://github.com/wodby/service-opensmtpd)

## What's included

| Component / service | Default configuration |
| --- | --- |
| Metabase<br>`metabase` | required; enabled by default; links: `postgres` → `postgres`, `sendmail` → `opensmtpd` |
| PostgreSQL<br>`postgres` | required; enabled by default; volumes: `data` 10 GB |
| OpenSMTPD<br>`opensmtpd` | optional; disabled by default |

Enabled optional services are selected by default but can be excluded when an
app is created. Disabled optional services are available but not selected by
default. Required services cannot be excluded.

## Validate the stack manifest

```bash
wodby stack validate-manifest stack.yml --org <org-id>
```

<!-- wodby:generated:end -->

## Deploy this stack

Set the Metabase service's Admin email and Admin password when creating the
application. The first deployment creates that administrator, so Metabase's
setup page is never open to the public. PostgreSQL holds Metabase's own data:
users, questions, dashboards and saved connections. Add the databases you want
to analyze in Metabase's admin settings.

Metabase sends invitations, password resets and dashboard subscriptions by
email. Enable OpenSMTPD, or enter your own SMTP server in Metabase's admin
settings.

Back up the PostgreSQL database before upgrading Metabase: newer versions
migrate it, and older versions can't use it afterwards.

## Maintain a custom version

1. Fork this repository.
2. Edit `stack.yml`.
3. Import the repository as a [Git-backed stack](https://wodby.com/docs/2.0/stacks/create/#create-a-git-backed-stack).

When replacing or renaming a stack service, update every related link target.
Stack-local names and referenced service names are distinct identifiers.
