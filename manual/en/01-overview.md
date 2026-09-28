# 1. Overview: create macros without coding

[한국어](../1.%20%EA%B8%B0%EB%8A%A5%EC%84%A4%EB%AA%85.md) | **English**

[Manual home](README.md) | [Contents](00-contents.md) | [Previous: 0](00-contents.md) | [Next: 2](02-editing-and-files.md)

Screenshots show the Korean interface; captions and instructions are in English.

## Overview

**JP's Codeless Macro Tool** is a free Windows automation tool for creating mouse and keyboard macros without writing code. Install the current version from Microsoft Store and receive updates through the Store. The last portable EXE released on GitHub is `v1.4.0`; use the Store edition for newer features.

Build an automation sequence one step at a time, or record your actions and turn them into steps.

## Main features

- Microsoft Store installation and automatic updates
- Korean and English interfaces, with automatic system-language selection
- Record clicks, key input, and drag paths with movement timing
- Mouse movement, clicks, double-clicks, dragging, and scrolling
- Mouse coordinate arrays that use a different position on each loop iteration, with grid generation and live previews
- Single keys and key combinations
- Automatic entry of long text, including Korean
- Comment steps for explaining your workflow
- Separate view and edit modes to reduce accidental changes
- Timed delays and waiting for clipboard changes
- Find buttons or regions by image matching, including OR searches across multiple images and movable, resizable capture regions with zoom previews
- Conditions for pixel colors, images, pressed keys, on-screen text, variable comparisons, and constant true/false values
- AND, OR, ELSE IF, ELSE, and conditional escape with BREAK
- Loops and nested loops
- Reusable blocks defined as pointers
- Variable assignment, calculations, text replacement, and selection variables with dropdown values
- Regular expressions to extract part of a string into a variable
- Built-in sample steps
- User-managed favorites
- Global play and stop hotkeys
- Background window input and compatibility modes for applications that are difficult to automate
- An Always on Top option to keep the control window visible
- Live variable and action-log monitors
- Pre-run validation of loops, conditions, pointers, and target settings
- Safety limits on executed steps, repetitions, pointer-call depth, and total runtime
- One previous valid project copy for recovery when opening a project fails

## Basic workflow

1. Launch the Store edition from the Start menu, or run `JPsCodelessMacroTool.exe` for the v1.4.0 portable edition.
2. Create a project name or open an existing project.
3. Add steps or record your actions.
4. Configure conditions, repetition counts, variables, regular expressions, or image searches as needed.
5. Save and play using the button or hotkey. If pre-run validation reports an error, fix the indicated step first.

![Main window with a sample macro](../img/1.-기능설명-01.png)

## Runtime monitors

Two monitor windows show progress while a macro runs. Toggle them with the buttons at the upper right.

- **Variable monitor**: displays current variable values in a table.
- **Log monitor**: displays each step's result with a timestamp, such as click coordinates, entered text, or a condition result.

Both windows snap next to the main window on its right and follow it when it moves or resizes. Detach them to place them freely. Enlarge the log monitor and scroll horizontally to read long messages.

Action logs are also written to files. Storage differs between the Store and portable editions. Use **Options → Open log folder** to open the active log location. See [Options and hotkeys](09-options-and-hotkeys.md).

## View update notes again

The What's New window shows new features and improvements after an update. To reopen it, choose **Help → What's New** in the main window. Notes from the Store launch version, `v1.4.0`, through the installed version are available offline.

## Suitable tasks

- Repetitive office data entry
- Repeated clicks on the same screen
- Branching when loading finishes or a popup appears
- Finding and clicking a button by its image even if its position changes
- Incrementing numbers or changing values between repetitions
- Clicking a different coordinate on each repetition
- Waiting for copied content before continuing
- Extracting only the needed values from screen or clipboard text with regular expressions

## Before you start

This tool controls the actual mouse and keyboard and can interfere with other work while running.

> [!WARNING]
> Games and some services may prohibit macros. Check the service's terms before using automation.

You are responsible for the results of your automation. When saving an existing project, the app keeps one previous valid copy so that you can recover if the file cannot be opened.

## Related guides

- [Recording and playback](03-recording-and-playback.md): turn real mouse and keyboard actions into a macro.
- [Image search and capture](08-image-search-and-capture.md): find and click buttons on screen.
- [App introduction and installation](../../README.en.md)
- [Full manual contents](00-contents.md)

## Continue reading

[Manual home](README.md) | [Contents](00-contents.md) | [Previous: 0](00-contents.md) | [Next: 2](02-editing-and-files.md)
