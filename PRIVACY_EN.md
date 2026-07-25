# Privacy Summary

[한국어](PRIVACY.md)

This is a Window (formerly TWMA) stores the information needed to restore window layouts only on this Mac.

## Information stored locally

- Workspace names and last-modified dates
- App names and bundle identifiers
- Titles, roles, ordering, and the last foreground app and window among ordinary windows visible on the active desktop when a workspace is created or updated
- Display identifiers, names, logical resolutions, arrangement, scale, rotation, and built-in status
- Per-display layouts and each window's target zone
- Whether an app may be launched, the selected automatic-restore workspace, optional workspace shortcuts, and the global pinned-layout shortcuts shared by slots 1–4 on every display
- Per-app Automatic, Position Only, and Excluded choices
- Language, drag-to-snap, preview style, Dock reservation, window gaps, automatic restore, launch-at-login, and automatic update-check preferences

Workspace data is stored at `~/Library/Application Support/TWMA/profiles-v1.json`. Creating a workspace records a new window set. Updating replaces that workspace's window list and positions. Renaming changes only its name, and deleting a workspace does not close or move open windows.

Other preferences and app-behavior policies remain in this Mac's existing TWMA preferences so the visible-name change preserves current settings. macOS manages the login item. Diagnostic compatibility results are not included in backups.

The Application Support directory uses `700` permissions and the profile file uses `600` permissions.

## Local diagnostic log

Technical drag and restore diagnostics are stored at `~/Library/Logs/TWMA.log`. The log does not include window titles, user-assigned workspace names, or URLs. To tie a running app to an exact build, the log records the app version, build number, bundle identifier, source commit ID, and clean or dirty source state. Restore and performance diagnostics may include a random restore-session ID, trigger, display and restored or missing window counts, an app bundle identifier, candidate-window count, and processing duration.

At 512 KB the log is rotated to one `TWMA.previous.log` file. Both files use `600` permissions.

## Information not collected or transmitted

- Accounts, passwords, keystrokes other than the shortcut combinations explicitly recorded by the user, or screen images
- Document contents inside windows
- Analytics, advertising, or tracking data
- Window, workspace, or diagnostic-log data uploaded to cloud or third-party servers

The app uses macOS Accessibility permission to inspect and move windows. Only ordinary app windows visible on the active desktop are saved.

## Update checks

Public builds check for new versions by default. Automatic checks can be disabled, and a manual check can be started, in General settings. The app requests `https://raw.githubusercontent.com/4celain/this-is-a-window/main/appcast.xml`. GitHub may process the connecting IP address, standard HTTP information, and the standard User-Agent containing the app, app version, and Sparkle version. The app disables system-profile transmission and does not append window, workspace, diagnostic-log, device-model, memory, or language information to the feed URL.

When an update is available, the signed DMG is downloaded from GitHub Releases. Installation and relaunch proceed only after user approval. The app does not use silent installation or delta updates. Development-bundle builds do not start the update service.

When the user selects a bug-report or support link in the app, the macOS default browser opens the configured external HTTPS page. The app does not attach or automatically send window or workspace data to that page.

## User-exported backups

A JSON backup created in Apps & Data contains:

- Saved workspace names, modified dates, optional shortcuts, and app, window, display, layout, and zone information
- Language, preview style, drag-to-snap, Dock reservation, window gaps, automatic restore, and automatic update-check preferences
- Default and per-display layouts, pinned menu layouts, the global shortcuts for slots 1–4, and selected automatic-restore workspaces
- App names, bundle identifiers, and placement modes
- Backup creation time, app version, and backup schema version

Accessibility permission, login-item state or approval, diagnostic logs, first-run acknowledgement, settings-window position, and the selected settings section are not included.

Backups are written only to the location chosen by the user and are not uploaded or synchronized. The app applies `600` permissions where the destination supports POSIX permissions. Imported profile and backup files larger than 8 MiB are rejected without replacing current data.

Individual workspaces can be deleted in Workspaces. To remove all workspace records, quit the app and delete `profiles-v1.json`; this does not delete separate preferences, app-behavior policies, or diagnostic logs.

This is a Window is publicly operated as `4celain`. Support and bug reports are handled through the [public distribution and support repository](https://github.com/4celain/this-is-a-window/issues/new?template=bug_report.yml).
