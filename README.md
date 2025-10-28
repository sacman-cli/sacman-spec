# sacman-spec

A specification defining the command-line interface and behavior for `sacman` implementations.

## What is `sacman`

`sacman` provides pacman-like command-line interface for basic `systemctl` usage.

Don't you think that the command-line of `systemctl` is tooooooo long?

## Status

Currently not stable. EVERYTHING might be changed. Discussion is welcomed.

## Usage

```
sacman SACMAN_OPTIONS [SYSTEMD_OPTIONS...] [NAME...]
```

**Attention**: 
- Currently sacman options must be combined like `-Styu` instead of `-S -t -y -u`
- Any other arguments will be passed directly to `systemctl`
- Order matters: sacman options first, then systemctl options

## Quick Examples

```bash
# systemctl --user enable mpris-proxy.service --now
sacman -Snu mpris-proxy

# systemctl status tlp  
sacman -Qi tlp

# systemctl restart tlp
sacman -Sty tlp

# systemctl list-units --type=service
sacman -Qy --type=service
```
## Available implementations

Currently NONE. If you implement one feel free to make a PR here. 
If you don't like `sacman-spec` standard you can also implement a `pacman-like` one and list it here with version=custom-*name*-va.b.c. 

| Implementation | Spec Version | Notes |
|---------------|--------------|--------|
| [sacman-py](https://github.com/sacman-cli/sacman-py) | v0.1 | quick example |

**Notes:**
- `Spec Version` indicates which version of this spec the implementation follows. See Release.
- Implementations may support extensions.

## spec

### Design


|Args|for|
|-|-|
|`-D` | systemctl `--dry-run` |
|`-S` | enable/start/unmask units |
|`-R` | disable/stop/mask units |
|`-Q` | Query units |
|`-F` | other unit File commands |
|`-T` | check (Test) |
|`-N` | eNvironment commands |
|`-J` | job commands |

### ALL


|Args| what |
|-|-|
| `-u` | `--user` |
| `-n` | `--now` |
| `-a` | `--all` |
| `-r` | `--recursive` |
| `-f` | `--force` |
| `-z` | dry-run of `sacman` (show the command will be executed) |

### -S


|Args| `systemctl` | why |
|-|-|-|
| `-S` | `enable` | pacman-like |
| `-Sy` | `reenable` | `y` for `re-`|
| `-Sd` | `reload` | reloaD |
| `-St` | `start` | *st*art |
| `-Sty` | `restart` | |
| `-Styc` | `condrestart` ||
| `-Styq` | `try-restart` |`q` for `try-`|
| `-Styd` | `reload-or-restart` ||
| `-Stydq` | `try-reload-or-restart` ||
| `-Sm` | `unmask` | Mask |

### -R


|Args| `systemctl` | why |
|-|-|-|
| `-R` | `disable` | pacman-like |
| `-Rc` | `clean` | pacman-like |
| `-Rt` | `stop` | Terminate |
| `-Rm` | `mask` | Mask |
| `-Rk` | `kill` | |
| `-Rv` | `revert` |


### -Q

|Args| `systemctl` | why |
|-|-|-|
| `-Ql` | `list-unit-files` |
| `-Qd` | `list-dependencies` |
| `-Qo` | `list-automounts` | 'ao' |
| `-Qm` | `list-machines` |
| `-Qt` | `list-timers` |
| `-Qp` | `list-paths` |
| `-Qk` | `list-sockets` |
| `-Qy` | `list-units` | 'yunit' |
| `-Qj` | `list-jobs` |
| `-Qi` | `status` |

### -F

|Args| `systemctl` | why |
|-|-|-|
| `-Fe` | `edit` |


### -T

|Args| `systemctl` | why |
|-|-|-|
| `-Ts` | `is-enabled` | s for enable |
| `-Tc` | `is-system-running` | c for system |
| `-Te` | `is-failed` | Error |

### -J
|Args| `systemctl` | why |
|-|-|-|
| `-Jl` | `list-jobs` |  |
| `-Jc` | `cancel` |  |

### -N
|Args| `systemctl` | why |
|-|-|-|
| `-N` | `show-environment` |  |
| `-Ns` | `set-environment` |  |
| `-Nn` | `unset-environment` |  |
| `-Ni` | `import-environment` |  |
