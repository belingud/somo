<p align="center">
  <img style="width: 250px" src="./images/somo-logo.png" />
</p>


### A human-friendly alternative to netstat for socket and port monitoring on Linux and macOS.


## ✨ Highlights:
- pleasing to the eye thanks to a nice table view
- filterable and sortable output
- interactive killing of processes
- JSON and custom formattable output
- from ``netstat -tulpn`` to ``somo -l``
- cross-platform support for Linux and macOS
- you can find all features further down

<br />

<p align="center">
  <img src="./images/somo-example.png" />
</p>

---

## ⬇️ Installation:

### Option 1 - Debian:
If you use a Debian OS go to [releases](https://github.com/theopfr/somo/releases) and download the latest .deb release.

### Option 2 - From crates.io:
```sh
cargo install somo
```
Most of the time you will want to run this in ``sudo`` mode to see all processes and ports. By default, this is not possible when installed via cargo. But you can create a symlink so the binary can be run as root:
```sh
sudo ln -s ~/.cargo/bin/somo /usr/local/bin/somo
sudo somo   # this works now
```
### Option 3 - Nix:

If you use Nix with Flakes, you can build and use the development version.

```sh
nix build 'github:theopfr/somo?dir=nix'
sudo ./result/bin/somo
```

---

## 🏃‍♀️ Running somo:
To run somo just type: 
```sh
sudo somo
```

Somo supports the following features:

### ✨ Filtering:
You can use the following flags to filter based on different attributes:
| filter flag | description | value |
| :------------- |:------------- | :----- |
| ```--tcp, -t``` | filter by TCP connections | - |
| ```--udp, -u``` | filter by UDP connections  | - | 
| ```--proto``` | deprecated – use ``--tcp`` / ``--udp`` instead | ``tcp`` or ``udp`` | 
| ```--port, -p``` | filter by a local port | port number, e.g ``5433`` |
| ```--remote-port``` | filter by a remote port | port number, e.g ``443`` |
| ```--ip``` | filter by a remote IP | IP address e.g ``0.0.0.0`` |
| ```--program``` | filter by a client program | program name e.g ``chrome`` |
| ```--pid``` | filter by a PID | PID number, e.g ``10000`` |
| ```--open, -o``` | filter by open connections | - |
| ```--listen, -l``` | filter by listening connections | - |
| ```--exclude-ipv6``` | don't list IPv6 connections | - |

### ✨ Compact table view:
To get a smaller, more compact table use the ``--compact, -c`` flag.

<img style="width: 75%" src="./images/somo-compact-example.png" />

### ✨ Process killing:
With the ``--kill, -k`` flag you can choose to kill a process after inspecting the connections using an interactive selection option.

<img style="width: 75%" src="./images/somo-kill-example.png" />

### ✨ JSON and custom output format:
Using the ``--json`` flag you can choose to retrieve the connection data in JSON format. <br />
You can also define a custom output format using the ``--format`` flag, for example:
```sh
somo --format "PID: {{pid}}, Protocol: {{proto}}, Remote Address: {{remote_address}}" # attributes must be specified in snake_case
```
In the format-string, the attributes have to be specified in *snake_case*.

### ✨ Sorting by columns:
The ``--sort, -s`` flag can be used to sort the table after a specific column ascending. For example:
```sh
somo --sort pid   # column names must be specified in snake_case
```
To get a descending order, you can use the ``--reverse, -r`` flag.

---

## 🐚 Shell Completions:
Somo supports shell completions for bash, zsh, fish, and elvish. Choose your shell:

### Bash
```bash
mkdir -p ~/.local/share/bash-completion/completions
somo generate-completions bash > ~/.local/share/bash-completion/completions/somo
```

### Zsh
```zsh
mkdir -p ~/.local/share/zsh/site-functions
somo generate-completions zsh > ~/.local/share/zsh/site-functions/_somo
echo 'fpath=(~/.local/share/zsh/site-functions $fpath)' >> ~/.zshrc
echo 'autoload -U compinit && compinit' >> ~/.zshrc
```

### Fish
```fish
mkdir -p ~/.config/fish/completions
somo generate-completions fish > ~/.config/fish/completions/somo.fish
```

### Elvish
```bash
mkdir -p ~/.config/elvish/lib
somo generate-completions elvish > ~/.config/elvish/lib/somo.elv
echo 'use somo' >> ~/.config/elvish/rc.elv
```

## 🖥️ Platform Support:
Somo currently supports:
- Linux: Full support using the procfs library
- macOS: Full support using libc and libproc libraries

We welcome contributions to extend support to other platforms!