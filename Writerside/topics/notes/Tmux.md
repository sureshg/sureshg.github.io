# Tmux

<primary-label ref="Linux"/>
<secondary-label ref="MacOS"/>

### Install Tmux

  ```bash
  $ brew install tmux
  # Tmux-based terminal divider
  $ brew install tmux-xpanes
  ```

### Save Tmux config

  ```bash
  $ tmux info
  $ tmux show -g | sed 's/^/set-option -g /' > ~/.tmux.conf

  ## Reload config
  $ tmux source ~/.tmux.conf

  # Kill Tmux server
  $ tmux kill-server
  ```

### [Basic Commands](https://github.com/tmux/tmux/wiki/Getting-Started#getting-started)

Prefix: <kbd>Ctrl</kbd>**-b**

* [Install Tmux Plugin manager](https://github.com/tmux-plugins/tpm#installation)

  ```bash
  # Install plugins
  $ prefix + I
  # Uninstall
  $ prefix + Alt + u
  ```
* [Save and Restore Sessions](https://github.com/tmux-plugins/tmux-resurrect#key-bindings)

  ```bash
  $ prefix + Ctrl-s
  $ prefix + Ctrl-r
  ```

* Manage Sessions

  ```bash
  $ tmux new -s code
  $ tmux attach-session -t code
  $ tmux kill-session -t code
  # Kill current session
  $ prefix + :kill-session
  # Detach a session
  $ prefix + d
  ```
* Windows and Sessions

  ```bash
  # Create a new window
  $ prefix + c

  # Rename a window
  $ prefix + ,

  # Kill a window
  $ Ctrl + d
  $ exit
  $ prefix + &

  # Switch to the previous window
  $ prefix + p
  # Switch to the next window
  $ prefix + n
  # Switch to window 1
  $ prefix + 1

  $ prefix + w
  $ tmux list-windows
  $ tmux list-sessions
  $ tmux list-clients
  $ tmux ls

  # Switch session
  $ prefix + s
  $ prefix + )
  $ prefix + (
  ```

* Window Panes

  ```bash
  # Split window vertically
  $ prefix + %
  # Split window horizontally
  $ prefix + '"'
  # Pane Navigation
  $ prefix + ->,<-,Up,Down
  # Exit pane
  $ exit or  prefix + x
  ```

* Show menu

  ```bash
  $ prefix +  >
  ```

* Mouse Mode

  Click <kbd>Alt/Option</kbd> to override the mouse protocol and let you select/paste

   ```bash
   set -g mouse on
   ```

Normally `Tmux` commands can be entered three different ways:

* By running `tmux ...`  command in a shell inside tmux
* By hitting <kbd>Ctrl</kbd>**-b + :** in tmux and then entering command into tmux’s command prompt
* By adding a command into to your `~/.tmux.conf` file to bind the key at startup

### [Key Bindings](https://www.seanh.cc/2020/12/28/binding-keys-in-tmux/)

* List Key Bindings

   ```bash
   $ prefix + ?
   $ tmux list-keys
   ```

### Modifier-Keys

* [Ctrl-Keys](https://github.com/tmux/tmux/wiki/Modifier-Keys#limitations-of-ctrl-keys)

