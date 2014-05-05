# Swap tmux panes easily

![](/img/demo.gif)

## Installation

### 1. Clone this repository and put swap-pane in your PATH

```
% git clone https://github.com/abicky/swap-pane.git
% cp swap-pane/swap-pane /path/to/your/bin/
```

### 2. Install percol

swap-pane depends on [percol](https://github.com/mooz/percol), so you must install it.

```
% pip install percol
```

You can also use `easy_install` to install percol.

```
% easy_install percol
```

### 3. Add the following lines in your .zshrc and .tmux.conf

#### .zshrc

```
autoload -U add-zsh-hook

if [ "$TMUX" ]; then
    function _set-pane-name() {
        local max_cmd_length=20
        local cmd=$1
        if [ $#cmd -gt $max_cmd_length ]; then
            cmd="${cmd:0:$max_cmd_length}..."
        fi
        printf "\033]2;${PWD/$HOME/~}: $cmd\033\\"
    }

    add-zsh-hook preexec _set-pane-name
    add-zsh-hook precmd _set-pane-name
fi
```

#### .tmux.conf

```
bind-key b new-window -nswap-pane 'swap-pane -t'
bind-key B run-shell 'swap-pane -n'
```


## Usage

Execute `swap-pane` command or type `<tmux prefix> b` to swap the current pane.

```
% swap-pane
```

`<tmux prefix> b` opens a temporary window to select an existing pane, so you can swap the current pane even if its process is not finished yet.

You can also execute `swap-pane -n` or type `<tmux prefix> B` to swap the current pane with a new pane.

```
% swap-pane -n
```


## Author

Takeshi Arabiki (abicky)


## Copyright and License

Copyright (c) 2014 Takeshi Arabiki licensed under the [MIT license](http://opensource.org/licenses/MIT).
