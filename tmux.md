# tmux

[tmux](https://github.com/tmux/tmux/wiki) is a terminal multiplexer. It lets you switch easily between several programs in one terminal, detach them (they keep running in the background) and reattach them to a different terminal.




### Commands

    $ tmux
      -u        # UTF8 mode
      -S ~/.tmux.socket

#### Sessions

    $ tmux new
    $ tmux new -s session_name

    $ tmux rename-session -t old-session-name new-session-name

    $ tmux attach # Default session
    $ tmux attach -t session_name

    $ tmux switch -t session_name

    $ tmux ls     # List sessions

    $ tmux detach

#### Windows

    $ tmux new-window

### Help

    C-b ?

### Scrolling

    C-b [       # Enter scroll mode then press up and down

### Copy/paste

    C-b [       # 1. Enter scroll mode first.
    Space       # 2. Start selecting and move around.
    Enter       # 3. Press enter to copy.
    C-b ]       # Paste

### Panes

    C-b %       # vert
    C-b "       # horiz
    C-b hkjl    # navigation
    C-b HJKL    # resize
    C-b o       # next window
    C-b q       # show pane numbers
    C-b x       # close pane

    C-b { or }  # move windows around

### Windows

    C-b c       # New window
    C-b ,       # Rename window
    C-b 1       # Go to window 1
    C-b n       # Go to next window
    C-b p       # Go to previous window
    C-b w       # List all window

### Detach/attach

    C-b d       # Detach
    C-b ( )     # Switch through sessions
    $ tmux attach

### Niceties

    C-b t    # Time

## Status formats

```
setw -g window-status-format `#[fg=8,bg=default]#I`
```

See `message-command-style` in the man page.

### Attribute/colors

| `#[fg=1]` | standard color |
| `#[fg=yellow]` | yellow |
| `#[bold]` | bold |
| `#[fg=colour240]` | 256 color |
| `#[fg=default]` | default |
| `#[fg=1,bg=2]` | combinations |
| `#[default]` | reset |

### Colors

 * `black` `red` `green` `yellow` `blue` `magenta` `cyan` `white`
 * `brightred` (and so on)
 * `colour0` ... `colour255`
 * `#333` (rgb hex)

### Attributes

 * `bold` `underscore` `blink` `noreverse` `hidden` `dim` `italics`

### Variables

| `#(date)` | shell command |
| `#I` | window index |
| `#S` | session name |
| `#W` | window name |
| `#F` | window flags |
| `#H` | Hostname |
| `#h` | Hostname, short |
| `#D` | pane id |
| `#P` | pane index |
| `#T` | pane title |

## Options

    set -g status-justify [left|centre|right]
    set -g status-left '...'

    setw -g window-status-style
    setw -g window-status-activity-style
    setw -g window-status-bell-style
    setw -g window-status-content-style
    setw -g window-status-current-style
    setw -g window-status-last-style

    setw -g window-status-format
    setw -g window-status-current-format

    setw -g window-status-separator

## 会话保存与恢复

- tmux Resurrect 会话手动保存与恢复
- tmux Continuum 会话定时保存自动恢复

### 安装插件

```
# 创建目录
mkdir ～/.tmux
cd ~/.tmux

# 下载插件
git clone https://github.com/tmux-plugins/tmux-resurrect.git
git clone https://github.com/tmux-plugins/tmux-continuum.git
## 若github网速不好，则可以使用gitee镜像，使用下述命令
git clone https://gitee.com/extra-mirrors/tmux-resurrect.git
git clone https://gitee.com/extra-mirrors/tmux-continuum.git

# 配置启用插件，编辑 ~/.tmux.conf
vim ~/.tmux.conf

# 将下述命令添加到.tmux.conf文件中
run-shell ~/.tmux/tmux-resurrect/resurrect.tmux
run-shell ~/.tmux/tmux-continuum/continuum.tmux

# Tmux Continuum 默认每隔 15 分钟备份一次，如果你频率过高，可以设置为 1 小时一次：
set -g @continuum-save-interval '60'

# 重载配置文件使之生效
tmux source-file ~/.tmux.conf
```

### 插件使用

- 手动保存tmux会话
  
    前缀键(C-b) + C-s

    此时 ，左下角 tmux 状态栏会显示 saving ... 字样 ， 完毕后会提示 Tmux environment saved字样表示 tmux 环境已保存 。
    Tmux Resurrect 会将 Tmux 会话的详细信息以文本文件形式保存到 ~/.tmux/resurrect 目录 。

- 手动还原tmux会话

    前缀键(C-b) + C-r
