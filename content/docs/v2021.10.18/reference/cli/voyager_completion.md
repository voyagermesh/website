---
title: Voyager Completion
menu:
  docs_v2021.10.18:
    identifier: voyager-completion
    name: Voyager Completion
    parent: reference-cli
menu_name: docs_v2021.10.18
section_menu_id: reference
info:
  cli: v0.0.3
  installer: v2021.10.18
  version: v2021.10.18
---

## voyager completion

Generate completion script

### Synopsis

To load completions:

Bash:

$ source <(kubectl-voyager completion bash)

# To load completions for each session, execute once:
Linux:
  $ kubectl-voyager completion bash > /etc/bash_completion.d/kubectl-voyager
MacOS:
  $ kubectl-voyager completion bash > /usr/local/etc/bash_completion.d/kubectl-voyager

Zsh:

# If shell completion is not already enabled in your environment you will need
# to enable it.  You can execute the following once:

$ echo "autoload -U compinit; compinit" >> ~/.zshrc

# To load completions for each session, execute once:
$ kubectl-voyager completion zsh > "${fpath[1]}/_kubectl-voyager"

# You will need to start a new shell for this setup to take effect.

Fish:

$ kubectl-voyager completion fish | source

# To load completions for each session, execute once:
$ kubectl-voyager completion fish > ~/.config/fish/completions/kubectl-voyager.fish


```
voyager completion [bash|zsh|fish|powershell]
```

### Options

```
  -h, --help   help for completion
```

### Options inherited from parent commands

```
      --enable-analytics   Send analytical events to Google Analytics (default true)
```

### SEE ALSO

* [voyager](/docs/v2021.10.18/reference/cli/voyager)	 - Voyager cli by AppsCode
