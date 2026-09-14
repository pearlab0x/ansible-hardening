# ansible-hardening

A tested Linux baseline and hardening collection. Every role is idempotent, linted, and verified in containers with Molecule, so no real hosts are needed to run or test it.

## Layout

```
ansible-hardening/
├── site.yml
├── roles/
│   ├── baseline/
│   ├── ssh_hardening/
│   ├── firewall/
│   └── auditd/
├── inventory/
│   ├── group_vars/all.yml
│   └── hosts.ini
├── molecule/
│   └── default/
│       ├── molecule.yml
│       ├── converge.yml
│       └── verify.yml
├── .github/workflows/ci.yml
├── .ansible-lint
├── requirements.yml
└── README.md
```

## Roles

`baseline` sets timezone, packages, and unattended upgrades.

`ssh_hardening` renders a locked down sshd_config and restarts the service through a handler.

`firewall` applies nftables rules from variables.

`auditd` installs audit rules for basic host visibility.

## Requirements

Ansible and Molecule with a container driver (Docker or Podman). Install the Python side with:

```bash
pip install ansible molecule molecule-plugins ansible-lint
```

## Usage

Run against your inventory:

```bash
ansible-playbook -i inventory site.yml
```

Preview changes without applying them:

```bash
ansible-playbook -i inventory site.yml --check --diff
```

## Testing

Molecule spins up a fresh container, applies the roles, then applies them again to prove nothing changes on the second pass.

```bash
molecule test
```

## License

MIT
