
# sclean — Deep System Cleanup Tool for Arch Linux / CachyOS


It removes:

- orphaned packages  
- package cache (pacman + yay)  
- old journal logs  
- Flatpak leftovers (runtimes, app data, cache)  
- browser caches (Chrome, Firefox, Brave, etc.)  
- thumbnail & shader caches  
- developer tool caches (npm, pip, cargo, go, etc.)  
- temporary files, trash, coredumps, crash reports  
- broken symlinks, stale processes, old logs, and more...



## Available Cleanup Categories

| Category            | Description                                          | Default? | Needs root? | Opt-in? |
|---------------------|------------------------------------------------------|----------|-------------|---------|
| `pacman`            | interrupted/corrupted downloads                      | yes      | yes         | no      |
| `orphans`           | unneeded dependencies                                | yes      | yes         | no      |
| `deep-orphans`      | orphans + optional deps                              | no       | yes         | yes     |
| `cache`             | pacman + yay package cache                           | yes      | yes         | no      |
| `journal`           | old systemd journal logs                             | yes      | yes         | no      |
| `flatpak`           | unused Flatpak runtimes                              | yes      | no          | no      |
| `flatpak-data`      | orphaned Flatpak app data (~/.var/app)               | yes      | no          | no      |
| `flatpak-cache`     | Flatpak temp/cache dirs                              | yes      | partial     | no      |
| `temp-files`        | old files in /tmp & /var/tmp                         | yes      | partial     | no      |
| `user-cache`        | ~/.cache files > 30 days + ~/.config backups         | yes      | no          | no      |
| `coredumps`         | systemd coredumps                                    | yes      | yes         | no      |
| `thumbnails`        | thumbnail cache                                      | yes      | no          | no      |
| `trash`             | empty trash bin                                      | yes      | no          | no      |
| `broken-symlinks`   | broken symlinks in $HOME (filtered)                  | yes      | no          | no      |
| `crash-reports`     | Electron/Chromium crash dumps                        | yes      | no          | no      |
| `mesa-shader`       | Mesa / RADV / NVIDIA / AMD shader cache              | yes      | no          | no      |
| `dev-caches`        | npm, pip, cargo, go, gradle, maven, etc.             | yes      | no          | no      |
| `old-logs`          | rotated/compressed logs in /var/log                  | yes      | yes         | no      |
| `browser-cache`     | Chrome, Firefox, Brave, Vivaldi cache                | yes      | no          | no      |
| `pacnew`            | show .pacnew / .pacsave files (info only)            | yes      | no          | no      |
| `systemd-failed`    | reset failed systemd units                           | yes      | yes         | no      |
| `service-leftovers` | clean broken systemd units & links                   | yes      | yes         | no      |
| `ram-cache`         | drop Linux page cache (frees RAM temporarily)        | no       | yes         | yes     |
| `stale-procs`       | kill processes using deleted executables             | no       | no          | yes     |



## Usage Examples


# Normal run (interactive, safe defaults)
sclean

# See what would be deleted (very recommended first!)
sclean -n

# Automatic + full cleanup
sclean -y

# Only clean caches & journals, no questions
sclean -y --only cache,journal

# Dry-run deep orphan removal
sclean -n --only deep-orphans

# Drop RAM cache (frees memory right now)
sclean --only ram-cache -y

# Skip Flatpak & dev caches
sclean --skip flatpak,dev-caches
