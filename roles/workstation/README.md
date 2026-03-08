# workstation role

Bootstraps a Linux workstation with a mix of distro packages, third-party repositories, direct-download tools, and user dotfiles.

## Structure

- `tasks/debian-base.yml`: apt cache management and baseline apt packages
- `tasks/debian-repositories.yml`: apt keyring and repository management
- `tasks/debian-desktop.yml`: desktop applications installed from apt or `.deb`
- `tasks/debian-containers.yml`: Docker engine and Compose plugin
- `tasks/debian-k8s.yml`: kubectl and minikube
- `tasks/binaries.yml`: Terraform, Terragrunt, Go, Helm, Helmfile, Neovim, shell config, and other binaries

## Important defaults

- `workstation_user`: local user that should own home-directory content
- `workstation_apt_full_upgrade`: opt-in full apt upgrade switch
- `workstation_apt_packages`
- `workstation_pip_packages`
- `workstation_npm_packages`
- `workstation_snap_packages`

## Assumptions

- The role is primarily built for Debian and Ubuntu.
- It expects privilege escalation for system package installation and writes into `/usr/local/bin`, `/opt`, and `/etc`.
- Several tools are intentionally pinned. Treat those pins as historical defaults, not current recommendations.
