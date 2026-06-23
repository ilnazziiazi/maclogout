# macout

Lock screen scheduler for macOS. Locks the screen during a configurable nighttime window and prevents unlocking until the window ends.

## How It Works

A LaunchDaemon (root) runs every second:
- Checks if current time is inside the configured window (default: 22:00–05:00)
- If inside window and screen is unlocked → locks screen (Ctrl+Cmd+Q equivalent)
- All apps keep running in the background

## Requirements

- macOS (Apple Silicon or Intel)
- Root access (sudo) for daemon installation

## Install

```bash
brew tap ilnazziiazi/macout
brew install macout
sudo cp $(brew --prefix)/opt/macout/launchd/com.macout.plist /Library/LaunchDaemons/
sudo launchctl load /Library/LaunchDaemons/com.macout.plist
```

## Configuration

```bash
macout --show              # view current config
sudo macout --start 23     # set start hour
sudo macout --end 6        # set end hour
macout --path              # show config file location
```

After changes, restart the daemon:
```bash
sudo launchctl unload /Library/LaunchDaemons/com.macout.plist
sudo launchctl load /Library/LaunchDaemons/com.macout.plist
```

## Logs

```bash
tail -f /var/log/macout.log
```

## Uninstall

```bash
sudo launchctl unload /Library/LaunchDaemons/com.macout.plist
sudo rm /Library/LaunchDaemons/com.macout.plist
brew uninstall macout
brew untap ilnazziiazi/macout
```

## License

MIT
