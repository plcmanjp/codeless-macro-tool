# 14. Background input: send input without bringing a window forward

[한국어](../14.%20%EB%B0%B1%EA%B7%B8%EB%9D%BC%EC%9A%B4%EB%93%9C%20%EC%9E%85%EB%A0%A5.md) | **English**

[Manual home](README.md) | [Contents](00-contents.md) | [Previous: 13](13-ocr.md)

Screenshots show the Korean interface; captions and instructions are in English.

## Background input

## What is background input?

Background input sends mouse and keyboard input directly to a target window without bringing it to the front. Ordinary macros normally send input to the foreground window. Background input lets you keep the target behind other windows, without minimizing it, while working elsewhere.

Examples include entering business-system data while reading email, keeping the target in a small corner window, or reducing window switching when automating several applications.

> [!NOTE]
> Background input works with standard Windows applications and some browsers. Applications with custom input handling may not support it.

## Select a target window

At the top of the main window, the background-input area contains a target-selection button and input-mode selector. Click the target button to open the selection dialog.

![Background target selection in the main window](../img/14.-백그라운드-입력-01.png)

### Method 1: click a window on screen

1. Choose Select a window by clicking on screen.
2. The screen dims while the window under the cursor is highlighted.
3. Move over the intended target and click.
4. The button changes to `Target: [program name]`, and the input-mode selector becomes available.

![Window-selection overlay](../img/14.-백그라운드-입력-05.png)

> [!TIP]
> Press Esc or right-click to cancel the overlay.

### Method 2: choose from a list

If clicking the window is inconvenient, select it from the list at the bottom of the dialog and confirm. Use Refresh list to reload currently open windows.

![Target-window selection dialog](../img/14.-백그라운드-입력-02.png)

### Clear the target

Click the assigned target button again to clear it. Playback then returns to ordinary input directed to the active window.

## Background input, compatibility mode, and Chrome text

After selecting a target, choose an input mode.

| Mode | Behavior | Suitable use |
| --- | --- | --- |
| Background input | Send input without bringing the target forward | Standard Windows apps and some browsers |
| Compatibility mode | Bring the target forward and send ordinary input | Apps that reject background input |
| Chrome text | Replace a selected web field's entire value without bringing Chrome forward; key steps do bring Chrome forward | Setting text in a Chrome web field |

Test Background input first. If text or keys do not arrive, try Compatibility mode. Compatibility mode brings the target to the foreground, so it is not fully background operation while you work in another window.

### Use Chrome text

1. Choose Select target window → Select by clicking on screen.
2. Click **directly on the web input field**, not an empty part of the Chrome window.
3. Choose Chrome text.
4. A text-input step replaces the field's entire current value with the step's text.

If navigation changes the window title, the target remains the same Chrome window and the app finds the field again on the current page. If the saved field cannot be matched but exactly one editable web field exists, it reconnects to that field.

> [!IMPORTANT]
> If several fields exist and the target cannot be determined safely, playback stops. Clear the target, then select it again by clicking the intended field directly.

In Chrome text mode, Key press, Key down, and Key up bring Chrome forward, focus the field, and execute. These keys are affected by the current Windows input-language/IME state.

Mouse move, click, down, up, and scroll steps do not run in Chrome text mode. Use Compatibility mode when mouse actions are required. The app does not guess another target or silently switch input to another window.

## Coordinates are relative to the target's client area

When a background target is assigned, registering coordinates with F2 or adding recorded actions stores coordinates relative to the target's **client area**. Moving the window on screen therefore preserves the point inside it, including when the window reopens at a different position.

> [!NOTE]
> Macros without a target still use absolute screen coordinates. Older projects retain their behavior unless you assign a target.

Background input also supports scrolling. A coordinate in a scroll step directs the message to that location inside the target. For a window with several lists, capture a position over the intended list.

## When the target window cannot be found

If the target is not open when registering F2 coordinates or adding a recording to the main window, the app shows a message and stops that operation. This avoids storing incorrect coordinates. Recorded actions are preserved.

Open the target application and try again.

### Target closes during playback

If the target closes during background playback, the app notifies you and stops the macro. Reopen the target, select it again, and restart playback.

## Targets running as administrator

When the target is elevated but the macro tool is not, playback may show an input-blocking warning. Windows' UIPI security boundary can block the input. Running the macro tool with administrator privileges can address this mismatch.

![Warning about input blocked for an elevated target](../img/14.-백그라운드-입력-06.png)

> [!WARNING]
> Review and test steps carefully before running with administrator privileges so automation does not unintentionally change system settings.

## Related input-compatibility features

The `v1.3.x` updates also added or improved the following.

### Scan-code keyboard compatibility

Some applications do not recognize ordinary simulated key input. Since `v1.3.0`, the app prefers standard Windows scan-code input for better compatibility. This applies automatically without extra settings; existing macros retain their key-input behavior.

### Relative mouse movement

Mouse click, down, and up steps have a Relative movement option. Move by **Δx/Δy from the current cursor position**, then perform the button action in one step.

Enabling it activates Δx, Δy, and movement-duration fields. A duration controls how long the cursor takes to reach its destination.

#### Fields

| Field | Description |
| --- | --- |
| Relative movement | Enable relative Δx/Δy mode; choose this or absolute movement, not both |
| Δx | Horizontal pixels: positive right, negative left |
| Δy | Vertical pixels: positive down, negative up |
| Movement duration, seconds | Zero moves immediately; duration applies to both absolute and relative movement |

![Relative movement enabled in the mouse-step editor](../img/14.-백그라운드-입력-03.png)

> [!NOTE]
> Relative movement is for foreground input only. With a background target assigned, a relative-movement step produces a warning and is skipped.

#### Example: move right and click

1. Add Mouse click.
2. Enable Relative movement.
3. Enter Δx `200` and Δy `0`.
4. Set a movement duration if needed.
5. Save.

Playback moves 200 pixels right from the current cursor position and clicks. The displacement stays the same regardless of the starting absolute coordinate.

### Full-screen capture with DXGI

Some full-screen applications previously produced black captures that prevented image matching or OCR. Since `v1.3.0`, the app prefers Windows desktop duplication (DXGI) to improve capture in those situations.

No separate setting is needed. Where DXGI is unavailable, it falls back to the previous capture method. Ordinary windowed-app capture remains unchanged.

## F2 coordinate-registration feedback

Pressing F2 in the main window briefly shows a green crosshair and coordinate information at the cursor. This lets you verify the captured point immediately.

![Crosshair and coordinates shown after F2 registration](../img/14.-백그라운드-입력-04.png)

## Example: enter data in a background business app

1. Open the data-entry application.
2. In the macro tool, click Select target window in the background-input area.
3. Choose on-screen selection and click the data-entry window.
4. Confirm that the button shows the selected application's name.
5. Try Background input first; use Compatibility mode if input is not accepted. For replacing a Chrome web field's complete value, reselect the target by clicking that field and choose Chrome text.
6. Register coordinates with F2 or record steps. Coordinates are stored relative to the target's client area.
7. Play. Background input leaves the target behind other windows; Compatibility mode brings it forward.

## Notes

### Supported and unsupported applications

Background input uses standard Windows input paths. It works with ordinary Windows desktop applications and some browsers. If it fails, try Compatibility mode. Applications using custom input such as DirectInput or RawInput may still reject input; clear the target and try ordinary input in that case.

### Check service terms

Check whether the target application permits automated input. Some online services prohibit macros.

> [!WARNING]
> Use the tool only for permitted repetitive tasks and within the target service's terms.

### Test before background use

It can be difficult to observe a background macro's effects. Test with the target visible in front first, then use background mode after confirming the actions.

### Avoid manual input to the same target

Using the mouse or keyboard directly in the target during background playback can mix your input with the macro's and produce unexpected results. Avoid interacting with that target while it runs.

## Related guides

- [Recording and playback](03-recording-and-playback.md)
- [Image search and capture](08-image-search-and-capture.md)
- [OCR](13-ocr.md)
- [Options and hotkeys](09-options-and-hotkeys.md)
- [App introduction and installation](../../README.en.md)
- [Full manual contents](00-contents.md)

## Continue reading

[Manual home](README.md) | [Contents](00-contents.md) | [Previous: 13](13-ocr.md)
