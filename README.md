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
brew tap <user>/maclogout
brew install maclogout
```

## Post-install

```bash
# Install and start the daemon
sudo cp /opt/homebrew/opt/maclogout/launchd/com.maclogout.plist /Library/LaunchDaemons/
sudo launchctl load /Library/LaunchDaemons/com.maclogout.plist

# Monitor
tail -f /var/log/maclogout.log
```

## Configuration

Edit `/opt/homebrew/etc/maclogout/config`:

```
START_HOUR=22   # Hour to start forcing logout (0–23)
END_HOUR=5      # Hour to stop (0–23). If < START_HOUR, wraps past midnight
```

## Stop / Uninstall

```bash
sudo launchctl unload /Library/LaunchDaemons/com.maclogout.plist
brew uninstall maclogout
brew untap <user>/maclogout
```

## License

MIT
