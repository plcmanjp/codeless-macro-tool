# 9. Options and hotkeys

[한국어](../9.%20%EC%98%B5%EC%85%98%EA%B3%BC%20%EB%8B%A8%EC%B6%95%ED%82%A4.md) | **English**

[Manual home](README.md) | [Contents](00-contents.md) | [Previous: 8](08-image-search-and-capture.md) | [Next: 10](10-favorites.md)

Screenshots show the Korean interface; captions and instructions are in English.

## Options and hotkeys

## Options

Use the Options window to adjust execution and editing defaults. Settings are stored in `app_config.json`: under `Documents\JPsCodelessMacroTool` for the Store edition, or beside the executable for the `v1.4.0` portable edition. Make normal changes through Options rather than editing this file directly.

![Hotkey settings in Options](../img/9.-옵션과-단축키-01.png)

## Theme

- **System**: follow the Windows light/dark setting.
- **Light**: always use the light theme.
- **Dark**: always use the dark theme.

## Change language

Choose the app's display language under **Language**.

| Option | Behavior |
| --- | --- |
| System | Follow the Windows display language using the rules below |
| 한국어 | Korean regardless of Windows settings |
| English | English regardless of Windows settings |
| 日本語 | Japanese regardless of Windows settings |
| 简体中文 | Simplified Chinese regardless of Windows settings |
| 繁體中文 | Traditional Chinese regardless of Windows settings |
| Español | Spanish regardless of Windows settings |
| Português (Brasil) | Brazilian Portuguese regardless of Windows settings |
| Deutsch | German regardless of Windows settings |
| Français | French regardless of Windows settings |

System language selection works as follows:

| Windows display language | Selected UI |
| --- | --- |
| Korean | Korean |
| Japanese | Japanese |
| Spanish | Spanish |
| Brazilian Portuguese | Brazilian Portuguese |
| German | German |
| French | French |
| Chinese in Taiwan, Hong Kong, or Macao | Traditional Chinese |
| Other Chinese locales | Simplified Chinese |
| Other languages | English |

Portuguese Windows locales outside Brazil, including Portugal, use English automatically.

Standard dialog buttons such as OK, Cancel, Yes, and No also use the selected language. A missing translation falls back to Korean for that item only. Changing the UI language does not change projects, favorites, text entered in macros, or the OCR recognition language.

Language changes take effect after restarting. After you confirm Options, the app asks whether to restart now and checks whether unsaved work should be saved first.

## Default shortcuts

| Function | Default |
| --- | --- |
| Play macro | F9 |
| Stop macro | F10 |
| Save | Ctrl+S |
| Capture coordinate | F2 |
| Auxiliary coordinate action: add row or calculate pitch | F3 |

Play and stop are global hotkeys. Editing shortcuts depend on the active window and editing context.

In coordinate entry, F2 captures the cursor immediately. Using the capture button captures the position after a three-second countdown.

In a mouse-step coordinate table, F3 appends the cursor's current position. The Add row button instead duplicates the selected coordinate. In the grid generator, F3 immediately starts endpoint capture for pitch calculation; using its button starts after a three-second countdown.

## Shortcuts while the app is inactive

Only execution-control shortcuts operate while the macro app is inactive:

| Default shortcut | Inactive behavior |
| --- | --- |
| F9 | Start playback |
| F10 | Stop playback |
| F7 | Start recording if the recorder is already open |
| F8 | Stop recording if the recorder is already open |
| F5 | Ignored |
| F2 | Ignored |
| ; | Ignored |

Shortcuts that change editing state, such as quick mouse registration, opening the recorder, and adding comments, require the app to be active.

## Change hotkeys

If another app uses the same keys, change them in Options. There are two groups:

- **Global hotkeys**: play, stop, open recorder, start/stop recording, and immediate mouse-move registration.
- **Editing hotkeys**: coordinate capture, default F2, and auxiliary coordinate action, default F3, in mouse-step editors.

When the app is behind other windows, only play/stop and start/stop recording with an open recorder operate. Opening the recorder with F5 and immediate mouse registration with F2 require the app to be active.

Hotkey conflicts with office apps, games, or browser extensions can cause unexpected actions. Assigning the same global hotkey to two functions produces a warning and prevents saving. Choose different keys and confirm again.

## Keyboard combinations

Since `v1.0.16`, keyboard action steps accept combinations, for example `ctrl+c`, `ctrl+v`, `shift+c`, and `ctrl+alt+delete`.

For copy-and-paste with a clipboard wait:

1. Add keyboard action `ctrl+c`.
2. Add a delay using Wait for clipboard change.
3. Add keyboard action `ctrl+v`.

This helps when the source app responds slowly.

## Global delay

Below the global-hotkey settings, set the short wait automatically inserted between executed steps when there is no explicit delay.

- Unit: milliseconds
- Default: `10 ms`
- Minimum: `1 ms`
- Maximum: `10000 ms`

An explicit delay step is not followed by an additional global delay.

## Always on top

Enable Always on Top to keep the main window and auxiliary windows, including variable and log monitors, above other windows even after clicking another application.

| State | Behavior |
| --- | --- |
| OFF | Default; other windows can cover the app |
| ON | Main and auxiliary windows stay on top |

![Always on Top and multiple-instance toggles](../img/9.-옵션과-단축키-02.png)

## Allow multiple instances

By default, only one instance runs. Launching again shows a notice instead of opening another window. Enable Allow multiple instances in Options to permit additional instances on subsequent launches.

| State | Behavior |
| --- | --- |
| OFF | Default; allow one instance |
| ON | Permit multiple windows on subsequent launches |

The setting is stored in `app_config.json` and applies to the next launch, not immediately to an already open window.

## Log files

The app writes execution records to a `logs` folder. Use **Open log folder** in Options to open the correct location in File Explorer.

| Edition | Log location |
| --- | --- |
| Microsoft Store | An app-specific folder under the user's LocalAppData |
| v1.4.0 portable | `logs` beside `JPsCodelessMacroTool.exe` |

| File | Content |
| --- | --- |
| `system.log` | Startup, update checks, errors, and other system activity |
| `{projectName}.log` | Step-by-step playback results, or action logs |

- Before the macro is saved, action logs use `untitled.log`; after saving, they use the project name.
- Restarting or opening another macro preserves the previous log as one `_prev.log` generation.
- The log monitor also shows action logs live. Open it from the upper-right button; it docks beside the main window along with the variable monitor.

Choose log verbosity in Options. Changes apply immediately without restarting.

| Level | Records |
| --- | --- |
| Auto | Default; uses INFO for normal operation |
| DEBUG | Detailed internal activity for investigation |
| INFO | Main actions such as playback, saving, and option changes |
| WARN | Situations requiring attention |
| ERROR | Errors only |

Use Options to change the level.

## Safe playback tips

- Test new macros with small repetition counts.
- Remember the stop hotkey.
- Avoid other work while a macro controls the actual mouse and keyboard.
- Validate with a test project before using it for important tasks.

## Related guides

- [Recording and playback](03-recording-and-playback.md)
- [Favorites](10-favorites.md)
- [App introduction and installation](../../README.en.md)
- [Full manual contents](00-contents.md)

## Continue reading

[Manual home](README.md) | [Contents](00-contents.md) | [Previous: 8](08-image-search-and-capture.md) | [Next: 10](10-favorites.md)
