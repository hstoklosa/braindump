# Autocomplete with up/down arrows (zsh)
Completion based on the prefix of your command is natively included in zsh. Simply include the following in your .zshrc (adjusting the bindkey keycodes if necessary for your OS):
```
autoload -U up-line-or-beginning-search
autoload -U down-line-or-beginning-search
zle -N up-line-or-beginning-search
zle -N down-line-or-beginning-search
bindkey "^[[A" up-line-or-beginning-search
bindkey "^[[B" down-line-or-beginning-search
```
