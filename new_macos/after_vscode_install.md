


## git & ~/.zsdhrc additional steps

### provides tabcomplete for branch names in git. 

run the following in a terminal and restart the terminal and/or vscode
```
echo 'autoload -Uz compinit && compinit' >> ~/.zshrc

source ~/.zshrc
```


### provides autocomplete when typing a few letters then hitting up.
#### what it does:
for example use the command 'flutter run ./lib/main.dart' then quit, then type 'cd ./' 
now typing 'flut' then up will go up to the most recent 'flutter run ./lib/main.dart'

#### how to:
Your ~/.zshrc has no key bindings and doesn't use Oh My Zsh, so you need to add them yourself. Add these lines to the end of ~/.zshrc:
```
# Up/Down arrows search history for commands starting with what's typed
autoload -U up-line-or-beginning-search down-line-or-beginning-search
zle -N up-line-or-beginning-search
zle -N down-line-or-beginning-search
bindkey "^[[A" up-line-or-beginning-search
bindkey "^[[B" down-line-or-beginning-search
bindkey "^[OA" up-line-or-beginning-search
bindkey "^[OB" down-line-or-beginning-search
```

#### How it works:

Type flut and press Up to jump to the most recent command starting with flut. Press Up again for the one before that, and Down to go forward.
With nothing typed, Up and Down work as before.
autoload and zle -N load two search functions that come with zsh.
bindkey attaches them to the arrow keys. Terminals send one of two codes for each arrow, so both are bound. That makes it work in VS Code's terminal and in Terminal.app.
There is also a built-in shortcut that needs no setup. Press Ctrl+R, type flut, and press Ctrl+R again to step back through earlier matches. It finds flut 
