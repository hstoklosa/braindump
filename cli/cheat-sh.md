# cheat.sh
Unified access to the best community driven cheat sheets repositories of the world.
## Command line client, cht.sh
The cheat.sh service has its `cht.sh` client that has several useful features compared to querying the service directly with `curl`
- Special shell mode with a persistent queries context and read-line support
- Queries history
- Clipboard integration
- Tab completion support for shells (bash, fish, zsh)
- Stealth mode
### Installation
For a user:
```
PATH_DIR="$HOME/bin"  # or another directory on your $PATH
mkdir -p "$PATH_DIR"
curl https://cht.sh/:cht.sh > "$PATH_DIR/cht.sh"
chmod +x "$PATH_DIR/cht.sh"
```

Globally:
```shell
curl -s https://cht.sh/:cht.sh | sudo tee /usr/local/bin/cht.sh && sudo chmod +x /usr/local/bin/cht.sh
```

### Client usage
Now, you can write your queries in more natural way (with spaces):
```
$   cht.sh go reverse a list
$   cht.sh python random list elements
$   cht.sh js parse json
```

It is even more convenient to start the client in a special shell mode:
```
$   cht.sh --shell
	  cht.sh> go reverse a list
```
or even start the client in this context:
```
$ cht.sh --shell go
    cht.sh/go> reverse a list
    ...
    cht.sh/go> join a list
    ...
```
If you want to change the context, you can do it with the `cd` command, or if you want do a single query for some other language, just prepend it with `/`:
```
$ cht.sh --shell go
	...
	cht.sh/go> /python dictionary comprehension
    ...
```
If you want to copy the last answer into the clipboard, you can use the `c` (`copy`) command, or `C` (`ccopy`, without comments).
```
cht.sh/python> append file
#  python - How do you append to a file?

with open("test.txt", "a") as myfile:
	myfile.write("appended text")
cht.sh/python> C
copy: 2 lines copied to the selection
```
Type `help` for other internal `cht.sh` commands.
```
cht.sh> help
	help    - show this help
	hush    - do not show the 'help' string at start anymore
	cd LANG - change the language context
	copy    - copy the last answer in the clipboard (aliases: yank, y, c)
	ccopy   - copy the last answer w/o comments (cut comments; aliases: cc, Y, C)
	exit    - exit the cheat shell (aliases: quit, ^D)
	id [ID] - set/show an unique session id ("reset" to reset, "remove" to remove)
	stealth - stealth mode (automatic queries for selected text)
	update  - self update (only if the scriptfile is writeable)
	version - show current cht.sh version
	/:help  - service help
	QUERY   - space separated query staring (examples are below)
				  cht.sh> python zip list
				  cht.sh/python> zip list
				  cht.sh/go> /python zip list
```

### Tab Completion
#### Bash
To activate tab completion support for `cht.sh`, add the `:bash_completion` script to your `~/.bashrc`
```bash
curl https://cheat.sh/:bash_completion > ~/.bash.d/cht.sh
. ~/.bash.d/cht.sh
# and add . ~/.bash.d/cht.sh to ~/.bashrc
```

#### ZSH
To activate tab completion support for `cht.sh`, add the `:zsh` script to the _fpath_ in your `~/.zshrc`
```bash
curl https://cheat.sh/:zsh > ~/.zsh.d/_cht
echo 'fpath=(~/.zsh.d/ $fpath)' >> ~/.zshrc
# Open a new shell to load the plugin
```
