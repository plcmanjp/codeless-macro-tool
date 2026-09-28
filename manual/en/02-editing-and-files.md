# 2. Basic editing and file management

[한국어](../2.%20%EA%B8%B0%EB%B3%B8%20%ED%8E%B8%EC%A7%91%EA%B3%BC%20%ED%8C%8C%EC%9D%BC%EA%B4%80%EB%A6%AC.md) | **English**

[Manual home](README.md) | [Contents](00-contents.md) | [Previous: 1](01-overview.md) | [Next: 3](03-recording-and-playback.md)

Screenshots show the Korean interface; captions and instructions are in English.

## Basic editing and file management

## Create a project

On first launch, create a project to store your macro. A project is a working unit containing steps and their related files.

Store projects are saved under `Documents\JPsCodelessMacroTool\script` by default. Use **Open path** in the project-open dialog to open the current project folder in File Explorer. The `v1.4.0` portable edition uses the `script` folder beside the executable.

## Add steps

A step is one action the macro performs, such as:

- Mouse click
- Keyboard input
- Text input
- Image search
- Condition start
- Loop start
- Delay

Add steps and fill in the required values to build your sequence.

## View mode and edit mode

Since `v1.0.24`, the app separates these modes:

- **View mode**: inspect and run steps.
- **Edit mode**: add, modify, delete, or move steps.

Newly created and opened projects start in view mode. Switch to edit mode to make changes. This helps prevent accidental edits before a run.

![Main window in view mode](../img/2.-기본-편집과-파일관리-01.png)

## Edit a step

Select an existing step to modify it. Since `v1.0.22`, selecting a row in the main step table and pressing `Enter` opens its editor.

Common edits include click coordinates, keyboard keys, text, wait duration, repetition count, condition values, and comments.

## Mouse action steps

There are five mouse actions:

| Step | Action | Typical use |
| --- | --- | --- |
| Mouse move | Move the cursor to a coordinate | Reposition without clicking |
| Mouse click | Press and release a button | Click buttons or select items |
| Mouse down | Hold a button down | Start a drag |
| Mouse up | Release a held button | End a drag |
| Mouse scroll | Scroll in the specified direction | Scroll lists or pages |

Most tasks need only Mouse click. Choose double-click in that step's options. Use Mouse down and Mouse up as a pair when a button must remain held.

To drag a file:

1. Move to the file.
2. Press the left button with Mouse down.
3. Move to the destination.
4. Release the left button with Mouse up.

![Mouse click step editor](../img/2.-기본-편집과-파일관리-02.png)

## Keyboard action steps

| Step | Action | Typical use |
| --- | --- | --- |
| Key press | Press and immediately release a key | Normal key input |
| Key down | Hold a key | Hold a modifier during another action |
| Key up | Release a held key | End a hold |

Key press is enough for most tasks, including combinations such as `ctrl+c` and `shift+tab`. Use Key down and Key up as a pair when other actions must happen while the key is held.

To select a range by Shift-clicking:

1. Click the first item.
2. Hold `shift` with Key down.
3. Click the last item.
4. Release `shift` with Key up.

## Text input steps

A text input step types a specified string. It accepts short words or long sentences containing Korean, English, numbers, and special characters.

Use `%variableName` in text to substitute a variable's value at runtime. Typing `%` opens a variable picker when variables have been declared. For example, if `N` is `001`, `Item%N` becomes `Item001`.

See [Variables and calculations](07-variables-and-calculations.md).

![Text input step editor](../img/2.-기본-편집과-파일관리-03.png)

## Delay steps

Delay steps wait before continuing. There are two types:

- **Timed wait**: add the hours, minutes, seconds, and milliseconds entered in the four fields.
- **Wait for clipboard change**: wait until the clipboard content changes. Continue when the maximum wait expires even if it has not changed.

For example, `1 hour 2 minutes 3 seconds 450 ms` is `3,723,450 ms`. Older macros' millisecond values are automatically displayed across these four fields when opened; saving and playback retain the same duration.

![Separate hour, minute, second, and millisecond fields](../img/2.-기본-편집과-파일관리-04.png)

Waiting for a clipboard change can help after a copy action such as `Ctrl+C`. For example, to copy an order number from a webpage and paste it into the next field:

1. Add a keyboard action for `ctrl+c`.
2. Add a delay and select Wait for clipboard change.
3. Set a maximum wait of about 1 to 3 seconds.
4. Follow it with `ctrl+v` or text input.

This reduces the chance of pasting before copying has finished.

## Enter mouse coordinates

Mouse move, click, down, and up steps use an inline coordinate table. Since `v1.0.43`, single coordinates and coordinate arrays share **one table**. It starts with one row; add rows to make an array.

### Coordinate-table buttons

| Button | Action |
| --- | --- |
| Capture (F2) | Enter the current cursor position immediately |
| Capture (3 sec) | Enter the cursor position after a three-second countdown |
| Add row | The button duplicates the selected coordinate; F3 adds the cursor's position at the moment you press it |
| Delete | Remove selected rows |
| Delete all | Clear the table and leave one empty row |
| Up / Down | Reorder selected rows |
| Auto-generate | Generate and append a grid of coordinates |

While editing, numbered points show the stored positions on screen in real time. Turn off **Coordinate preview** to hide them.

### How coordinate arrays work

Two or more rows form an array. Inside a loop, each iteration uses the next coordinate.

| Iteration | Coordinate |
| --- | --- |
| 1 | First |
| 2 | Second |
| 3 | Third |
| 4, with a three-coordinate array | First again |

To click matching buttons in three table rows:

1. Add Loop start with a count of `3`.
2. Add Mouse click.
3. Enter three coordinates, using Add row to duplicate a selected coordinate or F3 to capture the current cursor position.
4. Add Loop end.

The three iterations click the first, second, and third coordinates respectively. See [Loops](05-loops.md) for grid generation and more examples.

## Comment steps

Comments explain a macro without performing any action during playback. Use them to label sections or explain why steps were temporarily disabled. Press `;` in the step list to add a comment quickly.

| Step | Content |
| --- | --- |
| Comment | Sign-in process |
| Text input | Enter user ID |
| Text input | Enter password |
| Comment | Wait for the main screen |
| Delay | 1000 ms |

Comments do not change execution flow.

## Reorder steps

Steps run from top to bottom. Move steps up or down to adjust the sequence. You can select multiple steps to move or delete together.

## Save

Save your macro to open it again later. The default shortcut is `Ctrl+S`.

If you close the app or open another project with unsaved changes, a dialog asks whether to save. If you choose Save but saving fails or you cancel entering a name, the current work remains intact.

## Previous valid copy and project recovery

When saving an existing project, the app preserves the currently readable `script.json` as `script.json.prev`. Only one generation is kept. A project's first save has no previous file to preserve.

If the project cannot be opened, a recovery dialog appears. Choose **Restore previous valid copy** to restore the saved file as `script.json`, then try opening it again.

The problematic file is retained as `script.json.failed` for investigation. Keep a separate backup of important project folders because only one previous generation is retained.

> [!WARNING]
> After saving or recovery, reopen the project and briefly test the steps and target window. Confirm that the recovered file also passes pre-run validation.

## File layout

Since `v1.0.21`, the executable is named `JPsCodelessMacroTool.exe`.

| Edition | Settings, favorites, and projects | Logs |
| --- | --- | --- |
| Microsoft Store | `Documents\JPsCodelessMacroTool` | Use Open log folder in Options |
| v1.4.0 portable | Beside `JPsCodelessMacroTool.exe` | The `logs` folder beside the executable |

To back up or transfer Store-edition data, copy `app_config.json`, `favorites.json`, and the `script` folder from `Documents\JPsCodelessMacroTool`. Logs are execution records; open their folder from Options and preserve them separately only when needed.

## Product name change

MacroFlow was renamed JP's Codeless Macro Tool in `v1.0.21`. The workflow remains the same; the executable is `JPsCodelessMacroTool.exe`.

## Related guides

- [Loops](05-loops.md): repeat a task a fixed number of times.
- [Variables and calculations](07-variables-and-calculations.md): change values or sentences between repetitions.
- [App introduction and installation](../../README.en.md)
- [Full manual contents](00-contents.md)

## Continue reading

[Manual home](README.md) | [Contents](00-contents.md) | [Previous: 1](01-overview.md) | [Next: 3](03-recording-and-playback.md)
