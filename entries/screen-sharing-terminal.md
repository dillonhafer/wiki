## Enabled ScreenSharing from a terminal

At some point you may need VNC access to your remote mac, but you never enabled it. This will let you enable VNC (screen sharing) from a local or SSH connection.

```bash
sudo defaults write /var/db/launchd.db/com.apple.launchd/overrides.plist com.apple.screensharing -dict Disabled -bool false
sudo launchctl load /System/Library/LaunchDaemons/com.apple.screensharing.plist
```
