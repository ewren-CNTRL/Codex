# Omarchy Commands in the Terminal

A comprehensive guide for managing Omarchy window manager through terminal commands.

## Table of Contents

- [Overview](#overview)
- [Configuration Paths](#configuration-paths)
- [Backgrounds](#backgrounds)
- [Themes](#themes)
- [Keybindings](#keybindings)
- [Workspaces](#workspaces)
- [System Management](#system-management)
- [Troubleshooting](#troubleshooting)

## Overview

Omarchy is a lightweight window manager that can be configured and managed through terminal commands. This guide covers the most common operations you'll need to perform.

## Configuration Paths

Understanding Omarchy's directory structure:

```bash
# Main configuration directory
~/.config/omarchy/

# Themes directory
~/.config/omarchy/themes/

# User wallpapers
~/Pictures/Wallpapers/

# System configuration (if applicable)
/etc/omarchy/
```

## Backgrounds

### Adding a background to a pre-existing theme

Copy a wallpaper to a specific theme's background directory:

```bash
cp "/home/ewren/Pictures/Wallpapers/a_man_sitting_in_a_chair.png" "/home/ewren/.config/omarchy/themes/ash/backgrounds/"
```

### Setting a background for all themes

```bash
# Copy to the default backgrounds directory
cp "/home/ewren/Pictures/Wallpapers/background.png" "/home/ewren/.config/omarchy/backgrounds/"
```

### Listing available backgrounds

```bash
# List backgrounds for a specific theme
ls -la ~/.config/omarchy/themes/ash/backgrounds/

# List all available backgrounds
find ~/.config/omarchy/ -name "*.png" -o -name "*.jpg" -o -name "*.jpeg"
```

### Removing a background

```bash
# Remove from specific theme
rm ~/.config/omarchy/themes/ash/backgrounds/unwanted_background.png

# Remove from global backgrounds
rm ~/.config/omarchy/backgrounds/unwanted_background.png
```

## Themes

### Listing available themes

```bash
# List all installed themes
ls -la ~/.config/omarchy/themes/

# Show theme details
cat ~/.config/omarchy/themes/ash/theme.conf
```

### Switching themes

```bash
# Switch to a specific theme (if omarchy supports theme switching)
omarchy-theme set ash

# Or edit the main configuration
sed -i 's/theme=.*/theme=ash/' ~/.config/omarchy/omarchy.conf
```

### Creating a new theme

```bash
# Create new theme directory
mkdir -p ~/.config/omarchy/themes/mytheme/{backgrounds,configs}

# Copy base configuration from existing theme
cp ~/.config/omarchy/themes/ash/theme.conf ~/.config/omarchy/themes/mytheme/
```

### Backing up themes

```bash
# Backup all themes
tar -czf omarchy-themes-backup-$(date +%Y%m%d).tar.gz ~/.config/omarchy/themes/

# Backup specific theme
tar -czf ash-theme-backup.tar.gz ~/.config/omarchy/themes/ash/
```

## Keybindings

### Viewing current keybindings

```bash
# Display keybinding configuration
cat ~/.config/omarchy/keybindings.conf

# Search for specific keybinding
grep -i "mod4" ~/.config/omarchy/keybindings.conf
```

### Reloading configuration

```bash
# Reload Omarchy configuration
omarchy-reload

# Or send signal to reload (if supported)
pkill -SIGUSR1 omarchy
```

## Workspaces

### Managing workspaces

```bash
# List current workspaces (if omarchy provides this command)
omarchy-workspace list

# Switch to workspace
omarchy-workspace switch 2

# Create new workspace
omarchy-workspace create "Development"
```

## System Management

### Starting/Stopping Omarchy

```bash
# Start Omarchy
omarchy &

# Stop Omarchy
pkill omarchy

# Restart Omarchy
pkill omarchy && omarchy &
```

### Checking Omarchy status

```bash
# Check if Omarchy is running
ps aux | grep omarchy

# Check Omarchy logs
journalctl -u omarchy --follow

# Or check local logs
tail -f ~/.local/share/omarchy/logs/omarchy.log
```

### Installing/Updating

```bash
# Update from source (example)
cd ~/src/omarchy
git pull origin main
make && sudo make install

# Restart after update
pkill omarchy && omarchy &
```

## Troubleshooting

### Common Issues

#### Backgrounds not displaying

```bash
# Check if background file exists
ls -la ~/.config/omarchy/themes/ash/backgrounds/

# Verify file permissions
chmod 644 ~/.config/omarchy/themes/ash/backgrounds/*.png

# Check configuration syntax
omarchy-check-config
```

#### Configuration not loading

```bash
# Validate configuration file
cat ~/.config/omarchy/omarchy.conf

# Check for syntax errors
omarchy --validate-config

# Reset to default configuration
cp /etc/omarchy/omarchy.conf.default ~/.config/omarchy/omarchy.conf
```

#### Performance issues

```bash
# Check system resources
htop

# Monitor Omarchy memory usage
ps -o pid,ppid,cmd,%mem,%cpu -p $(pgrep omarchy)

# Check for error messages
dmesg | grep -i omarchy
```

### Useful Debugging Commands

```bash
# Run Omarchy in debug mode
omarchy --debug

# Check X11 compatibility
xwininfo -root -tree

# Verify display settings
xrandr --current
```

### Log Files

Common locations for Omarchy logs:

```bash
# User logs
~/.local/share/omarchy/logs/
~/.config/omarchy/logs/

# System logs
/var/log/omarchy/

# X11 logs
~/.local/share/xorg/Xorg.0.log
```

---

## Quick Reference

### Most Common Commands

```bash
# Add wallpaper to theme
cp "/path/to/image.png" "~/.config/omarchy/themes/THEME_NAME/backgrounds/"

# Reload configuration
omarchy-reload

# Check if running
ps aux | grep omarchy

# View logs
tail -f ~/.local/share/omarchy/logs/omarchy.log
```

### Configuration File Locations

| Component | Path |
|-----------|------|
| Main config | `~/.config/omarchy/omarchy.conf` |
| Keybindings | `~/.config/omarchy/keybindings.conf` |
| Themes | `~/.config/omarchy/themes/` |
| Backgrounds | `~/.config/omarchy/themes/THEME/backgrounds/` |
| Logs | `~/.local/share/omarchy/logs/` |

---

**Last updated:** August 2, 2025
