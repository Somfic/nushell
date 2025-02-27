# Nushell configuration files

## Installation

### MacOS / Linux
```
brew install nushell
```

### Windows
```
winget install nushell
```

### Third party tools needed

```
winget install ajeetdsouza.zoxide
winget install -e --id rsteube.Carapace
winget install --id Starship.Starship
winget install fastfetch
```


### config.nu changes
```nu
alias cd.. = cd ..
alias c = committer

alias cwr = cargo watch -q -c -x 'run -q'

# Zoxide
source .zoxide.nu

# Carapace
source .carapace.nu

# Starship
use .starship.nu

clear
fastfetch
```

### env.nu changes
```
cargo install committer

# Zoxide configuration
zoxide init nushell --cmd cd | save -f ~/nushell/.zoxide.nu

# Carapace configuration
$env.CARAPACE_BRIDGES = 'zsh,fish,bash,inshellisense' # optional
carapace _carapace nushell | save --force ~/nushell/.carapace.nu

# Starship configuration
starship init nu | save -f ~/nushell/.starship.nu

# Yazi
def --env yy [...args] {
	let tmp = (mktemp -t "yazi-cwd.XXXXXX")
	yazi ...$args --cwd-file $tmp
	let cwd = (open $tmp)
	if $cwd != "" and $cwd != $env.PWD {
		cd $cwd
	}
	rm -fp $tmp
}

# Default editor
$env.EDITOR = "nvim"
```
