# ansible-workstation

Legacy Ansible playbook for bootstrapping a Linux workstation.

This repository is organized as a single `workstation` role with task files split by concern:

- `debian-base.yml`: apt cache, core packages, and shared apt setup
- `debian-repositories.yml`: third-party apt keys and repositories
- `debian-desktop.yml`: GUI applications and desktop-specific installs
- `debian-containers.yml`: Docker engine and Compose plugin
- `debian-k8s.yml`: Kubernetes and minikube tooling
- `binaries.yml`: direct-download developer tools, shell, and editor config
- `pip.yml`, `npm.yml`, `snap.yml`: language- or package-manager-specific installs

## Usage

Run the playbook against the included localhost inventory:

```bash
ansible-playbook workstation.yml --ask-become-pass
```

Useful tags:

- `packages`
- `repositories`
- `desktop`
- `docker`
- `k8s`
- `binaries`
- `pip`
- `npm`
- `snap`

Examples:

```bash
ansible-playbook workstation.yml --tags docker,k8s --ask-become-pass
ansible-playbook workstation.yml --skip-tags snap --ask-become-pass
```

## Maintenance notes

- Most mutable lists now live in `roles/workstation/defaults/main.yml`.
- The repository is intentionally version-pinned in several places because it started as a personal bootstrap. Review pinned versions before using it on a current workstation.
- Full apt upgrades are disabled by default. Enable `workstation_apt_full_upgrade=true` only when you want that behavior.

## Validation

CI runs:

- `yamllint`
- `ansible-playbook --syntax-check`
- `ansible-lint`
