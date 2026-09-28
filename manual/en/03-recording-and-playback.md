# 3. Recording and playback

[한국어](../3.%20%EB%85%B9%ED%99%94%EC%99%80%20%EC%9E%AC%EC%83%9D.md) | **English**

[Manual home](README.md) | [Contents](00-contents.md) | [Previous: 2](02-editing-and-files.md) | [Next: 4](04-conditions.md)

Screenshots show the Korean interface; captions and instructions are in English.

## Recording and playback

## Recording

Recording captures your real mouse and keyboard actions and converts them into steps. It is useful for quickly sketching a macro's overall flow. After recording, shorten unnecessary delays and add conditions or loops to improve reliability.

If a recorded mouse position must change between repetitions, edit that mouse step into a coordinate array afterward.

![Recorder window](../img/3.-녹화와-재생-01.png)

## Recording example

Start with a recording, then refine it. To type a query and click a search button:

1. Start recording.
2. Click the search field.
3. Enter the query.
4. Click the search button.
5. Stop recording.
6. Remove unnecessary mouse movements from the generated steps.
7. If results appear slowly, adjust the wait with an image condition or a delay step.

## Record mouse drags

You can record movement while holding a mouse button. A drag records both its path and the time taken to move between points. Playback reproduces the path and speed, which also supports drawing tasks such as dragging in Paint.

**Pauses versus movement time**

Time spent stationary becomes a delay step. Time spent moving becomes the mouse step's movement duration. The descriptions of mouse move, click, down, and up steps include this duration.

**Recording option: mouse movement interval**

The mouse movement interval controls how densely a drag path is sampled. Its default is `300 ms`. Smaller values record more points; larger values reduce the number of steps.

> [!TIP]
> Reduce the interval when the path matters, such as freehand drawing or dragging a slider.

> [!NOTE]
> Mouse steps from older versions may lack movement-duration data. Such steps do not display a movement duration and play without one.

## Clean up a recording

Recorded steps can be used as they are, but these edits usually improve reliability:

- Shorten excessive delays.
- Consider waiting for a clipboard change after copying instead of using a fixed delay.
- Remove unnecessary mouse movement.
- Check click positions.
- Use coordinate arrays if each repetition needs a different position.
- Put repeated sections in loops.
- Add image conditions where actions depend on the screen state.

## Playback

Play a saved macro using the button or a global hotkey. The default hotkeys are:

- Play: `F9`
- Stop: `F10`

Change them in Options.

## Pre-run validation

Pressing Play or `F9` checks the macro before sending input. The check covers matching loop, condition, and pointer boundaries, missing images, target-window settings, and whether Chrome input combinations are supported by the selected input mode.

Errors appear in the **Pre-run validation error** dialog with the affected step and a suggested fix. No mouse or keyboard input starts until errors are fixed. If only warnings remain, review them and choose whether to continue.

For structure errors, review [Conditions](04-conditions.md) or [Pointers](06-pointers.md).

![Playback controls and repetition count](../img/3.-녹화와-재생-02.png)

## Repeated playback

Set a repetition count to run the same macro multiple times. Variables with reset-on-repeat enabled return to their initial values on every repetition. This setting can be chosen individually for each variable.

Safety limits apply to executed steps, repetition counts, pointer-call depth, and total runtime. Ordinary short macros are unaffected; unexpectedly long execution stops automatically at a limit. If a limit message appears, reduce repetitions or pointer nesting, or split the task into multiple projects.

Example: repeat a search five times with a changing query number.

1. Create `N` with initial value `001`.
2. Enter `Product%N` in a text input step.
3. Add a click on the search button.
4. Increment `N` by 1 with a variable calculation step.
5. Wrap the sequence in Loop start and Loop end with a count of `5`.

## Stop during playback

Press the stop hotkey while a macro runs. Because automation sends real input, stop immediately if it behaves unexpectedly.

Even after validation passes, test a short section first. If the target window or screen layout has changed, stop and update coordinates, images, and the target window.

## Global hotkeys

Global hotkeys work even when the app is behind other windows. If they conflict with another application's shortcuts, change the play and stop hotkeys in Options.

## Related guides

- [Loops](05-loops.md): repeat recorded actions.
- [Image search and capture](08-image-search-and-capture.md): find buttons whose positions change.
- [App introduction and installation](../../README.en.md)
- [Full manual contents](00-contents.md)

## Continue reading

[Manual home](README.md) | [Contents](00-contents.md) | [Previous: 2](02-editing-and-files.md) | [Next: 4](04-conditions.md)
