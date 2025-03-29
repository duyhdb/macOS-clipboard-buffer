# macOS-clipboard-buffer
Script works like Windows Clipboard Windows + V

# Clipboard Buffer Script - User Guide

## Overview

`clipboard_buffer.sh` is a script that saves and manages a history of copied clipboard contents on macOS. It allows users to retain multiple clipboard entries and retrieve them as needed.

## Features

- **Automatic Clipboard History**: Stores multiple copied items.
- **Persistent Storage**: Optionally save clipboard history even after a restart.
- **Command-Line Access**: Retrieve, list, or clear clipboard history using terminal commands.
- **Lightweight & Fast**: Runs efficiently in the background.

## Installation

1. **Download or create the script:**

   ```sh
   curl -o ~/clipboard_buffer.sh https://your-repository-url/clipboard_buffer.sh
   ```

   OR manually create `clipboard_buffer.sh` in your desired directory.

2. **Make the script executable:**

   ```sh
   chmod +x ~/clipboard_buffer.sh
   ```

3. **Move it to a system-wide accessible location (optional):**

   ```sh
   sudo mv ~/clipboard_buffer.sh /usr/local/bin/clipboard_buffer
   ```

## Usage

### **1. Start the Clipboard Buffer**

Run the script in the background:

```sh
./clipboard_buffer.sh &
```

Or if moved to `/usr/local/bin`:

```sh
clipboard_buffer &
```

### **2. Retrieve Clipboard History**

To display all saved clipboard entries:

```sh
cat ~/.clipboard_history
```

### **3. Restore a Previous Clipboard Entry**

Use `pbcopy` to restore a previous clipboard entry:

```sh
tail -n 5 ~/.clipboard_history | fzf | pbcopy
```

*(Requires **`fzf`** for interactive selection)*

### **4. Clear Clipboard History**

```sh
> ~/.clipboard_history
```

### **5. Auto-Run on Login (Optional)**

To keep the script running after system restart, set up a **LaunchAgent**:

1. Create a `.plist` file:
   ```sh
   mkdir -p ~/Library/LaunchAgents
   nano ~/Library/LaunchAgents/com.user.clipboard_buffer.plist
   ```
2. Add the following content:
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
   <plist version="1.0">
     <dict>
       <key>Label</key>
       <string>com.user.clipboard_buffer</string>
       <key>ProgramArguments</key>
       <array>
         <string>/usr/local/bin/clipboard_buffer</string>
       </array>
       <key>RunAtLoad</key>
       <true/>
       <key>KeepAlive</key>
       <true/>
     </dict>
   </plist>
   ```
3. Load the LaunchAgent:
   ```sh
   launchctl load ~/Library/LaunchAgents/com.user.clipboard_buffer.plist
   ```

## Uninstallation

To remove the script and its history:

```sh
rm -f ~/.clipboard_history ~/clipboard_buffer.sh
```

If using **LaunchAgent**, unload it:

```sh
launchctl unload ~/Library/LaunchAgents/com.user.clipboard_buffer.plist
rm -f ~/Library/LaunchAgents/com.user.clipboard_buffer.plist
```

## Troubleshooting

- **Script stops after sleep?** Use LaunchAgent or rerun `clipboard_buffer.sh &`.
- **Not capturing clipboard?** Ensure `pbpaste` and `pbcopy` work correctly.
- **Permission issues?** Run `chmod +x clipboard_buffer.sh`.

## License

MIT License. Feel free to modify and distribute.

---

*For updates and improvements, contribute at *[*GitHub Repository*](https://github.com/your-repo)*.*

