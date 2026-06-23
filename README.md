# maclogout

Force-logout scheduler for macOS. Logs out the current GUI user during a configurable nighttime window and prevents re-login until the window ends.

## How It Works

A LaunchDaemon (root) runs every 60 seconds:
- Checks if current time is inside the configured window (default: 22:00–05:00)
- If inside window and a GUI user is logged in → forces logout
- If user logs back in during the window → logs them out again on the next tick

## Requirements

- macOS (Apple Silicon or Intel)
- Root access (sudo) for daemon installation

## Install

```bash
brew tap ilnazziiazi/maclogout
brew install maclogout
sudo cp $(brew --prefix)/opt/maclogout/launchd/com.maclogout.plist /Library/LaunchDaemons/
sudo launchctl load /Library/LaunchDaemons/com.maclogout.plist
```

## Configuration

```bash
maclogout --show              # view current config
sudo maclogout --start 23     # set start hour
sudo maclogout --end 6        # set end hour
maclogout --path              # show config file location
```

After changes, restart the daemon:
```bash
sudo launchctl unload /Library/LaunchDaemons/com.maclogout.plist
sudo launchctl load /Library/LaunchDaemons/com.maclogout.plist
```

## Logs

```bash
tail -f /var/log/maclogout.log
```

## Uninstall

```bash
sudo launchctl unload /Library/LaunchDaemons/com.maclogout.plist
sudo rm /Library/LaunchDaemons/com.maclogout.plist
brew uninstall maclogout
brew untap ilnazziiazi/maclogout
```

## License

MIT
