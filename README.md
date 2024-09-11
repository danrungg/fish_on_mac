# Installing Fish Shell on macOS using Homebrew

## Installation Steps

### 1. Install Fish

```bash
brew install fish
```

### 2. Find Fish shell path

```bash
which fish
```

### 3. Set Fish as the default shell

1. Open Terminal and run:
   ```bash
   sudo nano /etc/shells
   ```

2. Add the output of `which fish` to the end of the file. It should look similar to this:

   ```
   # List of acceptable shells for chpass(1).
   # Ftpd will not allow users to connect who are not using
   # one of these shells.
   /bin/bash
   /bin/csh
   /bin/dash
   /bin/ksh
   /bin/sh
   /bin/tcsh
   /bin/zsh
   /opt/homebrew/bin/fish
   ```

3. Save and exit the terminal.

4. Change the default shell:
   - Open System Settings
   - Go to Users & Groups
   - Right-click on your username > Advanced Options...
   - In the Login Shell dropdown menu, select the Fish shell

### 4. Add Homebrew to Fish path

```fish
fish_add_path /opt/homebrew/bin
```

### 5. Update Fish completions

```fish
fish_update_completions
```

### 6. Configure Fish

```fish
fish_config
```

### 7. Add `cdf` functionality (very useful!)

This function allows you to change to the current Finder directory.

1. Navigate to Fish functions directory:
   ```fish
   cd ~/.config/fish/functions/
   ```

2. Create this file:
   ```fish
   touch cdf.fish
   ```

3. Open the file in nano:
   ```fish
   nano cdf.fish
   ```

4. Add this code:
   ```fish
   function pfd -d "Return the path of the frontmost Finder window"
     osascript 2>/dev/null -e '
       tell application "Finder"
         return POSIX path of (target of window 1 as alias)
       end tell'
   end

   function cdf -d "cd to the current Finder directory"
     cd (pfd)
   end
   ```
