# TMUX Configuration

This repository contains a customized TMUX configuration that enhances the usability and appearance of TMUX. This configuration is designed to make your terminal experience more efficient and visually appealing. Below, you'll find a detailed explanation of the configurations and how to use them.

## Installation

1. **Clone the repository**:
   ```bash
   https://github.com/hardsoftsecurity/Tmux-Configuration.git
   ```

2. **Navigate to the directory**:
   ```bash
   cd tmux-config
   ```

3. **Copy the configuration file to your home directory**:
   ```bash
   cp tmux.conf ~/.tmux.conf
   ```

4. **Reload TMUX configuration**:
   ```bash
   tmux source-file ~/.tmux.conf
   ```

## Configuration Details

### Change Prefix Key
- **New Prefix**: `Ctrl-a`
  - This changes the default prefix from `Ctrl-b` to `Ctrl-a`.
  ```tmux
  unbind C-b
  set-option -g prefix C-a
  bind-key C-a send-prefix
  ```

### Enable Mouse Mode
- **Mouse Mode**: Allows the use of the mouse for resizing panes, scrolling, and selecting text.
  ```tmux
  set -g mouse on
  ```

### Vi Mode Selection
- **Set Vi Mode for Copy Mode**: Enables Vi-style key bindings for selecting and copying text.
  ```tmux
  set-window-option -g mode-keys vi
  bind-key -T copy-mode-vi 'v' send -X begin-selection
  bind-key -T copy-mode-vi 'y' send -X copy-selection-and-cancel
  ```

### Clipboard Integration
- **Copy and Paste with Clipboard**:
  ```tmux
  bind C-c choose-buffer "run \"tmux save-buffer -b '%%' - | xsel -i -b\""
  bind C-v run "xsel -o -b | tmux load-buffer - && tmux paste-buffer"
  bind C-y choose-buffer "run \"tmux save-buffer -b '%%' - | xsel -i\""
  bind C-p run "xsel -o | tmux load-buffer - && tmux paste-buffer"
  ```

### Status Bar Appearance
- **Customize Status Bar Colors**:
  ```tmux
  set -g status-style bg=colour33,fg=colour196  # Bright blue background, bright red text
  set -g status-left '#[fg=colour226,bg=colour33,bold] #S '
  set -g status-right '#[fg=colour196,bg=colour33] %Y-%m-%d #[fg=colour196,bg=colour33] %H:%M:%S '
  ```

### Window and Pane Colors
- **Active and Inactive Windows**:
  ```tmux
  setw -g window-status-current-style bg=colour160,fg=colour231,bold
  setw -g window-status-style bg=colour33,fg=colour226
  setw -g window-status-activity-style bg=colour1,fg=colour231,bold
  ```
- **Pane Borders**:
  ```tmux
  set -g pane-border-style fg=colour45  # Bright blue border
  set -g pane-active-border-style fg=colour51  # Bright cyan border
  ```

### Command and Copy Mode Colors
- **Command Messages**:
  ```tmux
  set -g message-style bg=colour28,fg=colour226  # Dark green background, bright yellow text
  ```
- **Copy Mode**:
  ```tmux
  setw -g mode-style bg=colour28,fg=colour226  # Dark green background, bright yellow text
  ```

### Usability Enhancements
- **History Limit**: Increase scrollback buffer.
  ```tmux
  set -g history-limit 10000
  ```
- **Monitor Activity**: Enable visual activity monitoring.
  ```tmux
  setw -g monitor-activity on
  set -g visual-activity on
  ```

### Additional Shortcuts
- **Reload Configuration**:
  ```tmux
  bind r source-file ~/.tmux.conf \; display-message "Configuration reloaded!"
  ```
- **Split Panes**:
  ```tmux
  bind | split-window -h
  bind - split-window -v
  ```
- **Synchronize Panes**:
  ```tmux
  bind-key S setw synchronize-panes
  bind-key s setw synchronize-panes off
  ```

### Interactive Shell Shortcuts
- **Python Shell**:
  ```tmux
  setenv -g py3 "python3 -c 'import pty;pty.spawn(\"/bin/bash\")'"
  setenv -g shellexports "export TERM=xterm"
  bind C-q send $py3 Enter
  bind -n C-q send "stty raw -echo; fg" Enter $shellexports Enter
  ```

## Usage

To start using the configurations, simply open a new TMUX session:
```bash
tmux
```

### Key Bindings

- **Prefix Key**: `Ctrl-a`
  - This is the new prefix key for TMUX commands. Press `Ctrl-a` followed by the desired command key.

- **Mouse Mode**: Enabled
  - Use the mouse to resize panes, scroll, and select text.

- **Vi Mode**: Enabled
  - Use Vi-style key bindings in copy mode (`v` to begin selection, `y` to copy selection).

- **Clipboard Integration**:
  - `Ctrl-c`: Copy selected text to clipboard.
  - `Ctrl-v`: Paste from clipboard.
  - `Ctrl-y`: Copy to primary clipboard.
  - `Ctrl-p`: Paste from primary clipboard.

- **Status Bar**: Customized with bright blue background and bright red text.
  - Left: Session name.
  - Right: Date and time.

- **Window and Pane Colors**:
  - Active Window: Bright red background, white text.
  - Inactive Window: Bright blue background, bright yellow text.
  - Pane Borders: Bright blue for inactive, bright cyan for active.
  - Command Messages: Dark green background, bright yellow text.
  - Copy Mode: Dark green background, bright yellow text.

- **Additional Shortcuts**:
  - `Ctrl-a r`: Reload TMUX configuration.
  - `Ctrl-a |`: Split window horizontally.
  - `Ctrl-a -`: Split window vertically.
  - `Ctrl-a S`: Synchronize panes.
  - `Ctrl-a s`: Disable synchronization of panes.

- **Interactive Shell Shortcut**:
  - `Ctrl-q`: Start an interactive Python shell.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.

## Acknowledgements

This configuration was inspired by various TMUX configurations available online. Special thanks to the TMUX community for their contributions and shared knowledge.

---

Feel free to contribute to this repository by opening issues or submitting pull requests with improvements and suggestions.
