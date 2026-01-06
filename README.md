# Ansible Collection - koyashiro.debian_base

Baseline Ansible collection for Debian systems.

## Requirements

- Ansible >= 2.18.0
- Target: Debian (bookworm)

## Dependencies

- `community.general` >= 5.0.0

## Installation

### From GitHub

```bash
ansible-galaxy collection install git+https://github.com/koyashiro/ansible-collection-debian-base.git
```

## Roles

### baseline

Applies all baseline configurations. This role includes all other roles as dependencies.

### locale

Configures system locale.

| Variable | Default         | Description   |
| -------- | --------------- | ------------- |
| `locale` | `"en_US.UTF-8"` | System locale |

### timezone

Configures system timezone.

| Variable   | Default        | Description     |
| ---------- | -------------- | --------------- |
| `timezone` | `"Asia/Tokyo"` | System timezone |

### hostname

Sets the system hostname.

| Variable   | Default                      | Description     |
| ---------- | ---------------------------- | --------------- |
| `hostname` | `"{{ inventory_hostname }}"` | Hostname to set |

### packages

Installs base packages.

| Variable         | Default     | Description                      |
| ---------------- | ----------- | -------------------------------- |
| `base_packages`  | (see below) | List of base packages to install |
| `extra_packages` | `[]`        | Additional packages to install   |

Default `base_packages`:

- vim, curl, wget, git, rsync
- dnsutils, tcpdump, lsof, htop
- file, tree, bash-completion

### editor

Sets the default editor.

| Variable      | Default                | Description            |
| ------------- | ---------------------- | ---------------------- |
| `editor_path` | `"/usr/bin/vim.basic"` | Path to default editor |

### ssh

Configures SSH server.

| Variable                | Default | Description                      |
| ----------------------- | ------- | -------------------------------- |
| `ssh_port`              | `22`    | SSH port                         |
| `ssh_permit_root_login` | `"no"`  | Allow root login                 |
| `ssh_pubkey_auth`       | `true`  | Enable public key authentication |
| `ssh_password_auth`     | `false` | Enable password authentication   |

## Usage

```yaml
---
- name: Apply baseline configuration
  hosts: all
  become: true
  roles:
    - role: koyashiro.debian_base.baseline
      # vars:
      #   hostname: "example"
      #   locale: "ja_JP.UTF-8"
      #   timezone: "Asia/Tokyo"
      #   extra_packages:
      #     - neovim
```

## License

MIT
