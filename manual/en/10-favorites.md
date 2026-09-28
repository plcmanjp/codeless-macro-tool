# 10. Favorites: reuse frequently used steps

[한국어](../10.%20%EC%A6%90%EA%B2%A8%EC%B0%BE%EA%B8%B0.md) | **English**

[Manual home](README.md) | [Contents](00-contents.md) | [Previous: 9](09-options-and-hotkeys.md) | [Next: 11](11-regex-extraction.md)

Screenshots show the Korean interface; captions and instructions are in English.

## Favorites

## What are favorites?

Favorites store frequently used steps for quick insertion later. Save common clicks, delays, text input, and conditions to speed up macro authoring.

## Add a favorite

Select the steps you use often and register them as a favorite. Give the favorite a recognizable name.

## Use a favorite

Select a favorite from the main window to add it to the current macro. You can also drag and drop it at the desired position.

## Manage favorites

Use the favorites management window to inspect and organize saved items. Since `v1.0.15`, adding a duplicate name prompts you to overwrite it or enter another name.

![Favorites management window](../img/10.-즐겨찾기-02.png)

## Favorites versus sample steps

Since `v1.0.23`, built-in examples are provided separately as **Sample steps**. Favorites are your personal collection of reusable steps. New users can try built-in examples from Sample steps first.

## Storage file

Favorites are stored in `favorites.json`. Include this file when moving your favorites to another PC.

## Uses

- Frequently used delays
- Click patterns
- Common text input
- Conditions for closing popups
- Image checks followed by clicks
- Basic loop-start and loop-end groups

## Examples

**Save a document, then wait briefly**

1. Add keyboard action `ctrl+s`.
2. Add a timed delay of about `300 ms`.
3. Select both steps and save a favorite named `Save and wait`.
4. Insert it wherever another macro needs to save.

**Close a recurring notification**

1. Add an image condition that detects the notification.
2. Put a close-button click inside it.
3. Save the condition block as a favorite.
4. Insert it at points where notifications may appear during a long macro.

## Related guides

- [Sample steps](12-sample-steps.md): insert built-in examples.
- [Basic editing and file management](02-editing-and-files.md)
- [App introduction and installation](../../README.en.md)
- [Full manual contents](00-contents.md)

## Continue reading

[Manual home](README.md) | [Contents](00-contents.md) | [Previous: 9](09-options-and-hotkeys.md) | [Next: 11](11-regex-extraction.md)
