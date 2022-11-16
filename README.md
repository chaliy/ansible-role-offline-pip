# Offline `pip` Ansible Role

[![Stand With Ukraine](https://raw.githubusercontent.com/vshymanskyy/StandWithUkraine/main/banner2-direct.svg)](https://vshymanskyy.github.io/StandWithUkraine/)


Install Python pip into air-gapped and offline environments

## Requirements

- Tested and probably requires Python 3
- Requires pip source archive somewhere on the local computer. See example how to specify

## Role Variables

Check `defaults/main.yml` for all variables.

## How to use

0. Install

```sh
ansible-galaxy install chaliy.offline_pip
```

1. Download pip source archive. For example, from https://pypi.org/project/pip/#files

```sh
mkdir ./.offline
wget https://files.pythonhosted.org/packages/ce/ea/9b445176a65ae4ba22dce1d93e4b5fe182f953df71a145f557cffaffc1bf/pip-19.3.1.tar.gz -P ./.offline
```

2. Optionally download wheels

```sh
pip wheel --wheel-dir=./.offline/wheels docker jsondiff
```

3. Specify `pip_tar_path`, `pip_wheels_path` and `pip_names` in your playbook
4. Run playbook

NOTE: [offline-playbook.yml](./hacks/offline-playbook.yml) is an example playbook that downloads pip and wheels offline

## Example Playbook

```yaml
- hosts: all
  roles:
  - role: chaliy.offline_pip
    pip_tar_path: ./.offline/pip-19.3.1.tar.gz
```

```yaml
- hosts: all
  roles:
  - role: chaliy.offline_pip
    pip_tar_path: ./.offline/pip-19.3.1.tar.gz
    pip_wheels_path: ./.offline/wheels
    pip_names:
    - docker
    - jsondiff
```

## Development

```sh
poetry install
make test
```

## License

MIT (Except russians)
