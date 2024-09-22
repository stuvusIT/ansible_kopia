# Kopia

This role installs [kopia](https://kopia.io/) and configures it for backups.
It was developed and tested with Debain, but it might work with other Debian based distributions.


## Requirements

The role doesn't initialize the repository for backups, you need to provide the correct configuration for an existing backup repository.
The default `kopia_repository_config` assumes a setup, where backups are proxied over a [repostory server](https://kopia.io/docs/repository-server/).
If you need a different kind of repository, you will need to adjust the config accordingly.
Creation of appropriate user accounts on the repository server is also beyond the scope of this role.

Additionally, the provided `kopia_ignore_patterns` are placed in `/etc/kopia/.kopiaignore`.
Your global policy (or a local one, if you want to configure this on a per-host basis) needs to include that in the dot-ignore list.


## Role Variables


| Name                        |               Required/Default                | Description                                                          |
| --------------------------- | :-------------------------------------------: | -------------------------------------------------------------------- |
| `kopia_api_server_url`      |           `http://localhost:51515`            | URL of the repository server to use. Not used, if config is replaced |
| `kopia_repository_password` |              :heavy_check_mark:               | Pasword for the repository.                                          |
| `kopia_backup_schedule`     |                `*-*-* 4:00:00`                | `OnCalendar` expression for the systemd timer triggering snapshots.  |
| `kopia_repository_config`   | See [defaults/main.yml](./defaults/main.yml). | Kopia repository config.                                             |
| `kopia_ignore_patterns`     | See [defaults/main.yml](./defaults/main.yml). | Patterns to ignore while taking snapshot.                            |

## Example

The following example playbook assumes that you cloned this role to `roles/kopia` (i.e. the name of the role is `kopia` instead of `ansible_kopia`).

```yml
- hosts: example01
  roles:
    - role: kopia
        kopia_repository_password: secret
        kopia_api_server_url: https://backup.example.com
```


## License

This work is licensed under the [MIT License](./LICENSE).


## Author Information

- [Sven Feyerabend (SF2311)](https://github.com/SF2311) Sven.Feyerabend at stuvus.uni-stuttgart.de_
