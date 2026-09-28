# 8. Image search and capture

[한국어](../8.%20%EC%9D%B4%EB%AF%B8%EC%A7%80%20%EA%B2%80%EC%83%89%EA%B3%BC%20%EC%BA%A1%EC%B2%98.md) | **English**

[Manual home](README.md) | [Contents](00-contents.md) | [Previous: 7](07-variables-and-calculations.md) | [Next: 9](09-options-and-hotkeys.md)

Screenshots show the Korean interface; captions and instructions are in English.

## Image search and capture

## What is image search?

Image search finds a specified image on screen and uses its position for actions. Find and click a button or icon, or capture an area and use its appearance to decide when to continue. This helps with applications and webpages whose button positions vary.

## Capture a reference image

For image conditions or image-based clicks, capture a screen region as a reference. Prefer distinctive buttons, icons, or text over a large area.

## Image conditions

Use image presence or absence to:

- Click only when a button is visible.
- Continue when loading finishes.
- Close an error popup.
- Refresh only when an image is absent.

To continue after a save-complete message:

1. Capture distinctive text or an icon in the message.
2. Add an image condition using that image.
3. Put the next-button click or close-window action inside the condition.
4. If the message is absent, those steps do not run.

## Find any of several images: OR search

When a button or icon has several possible appearances, register multiple images in one condition.

- Images appear in a list.
- List order sets search priority; searching starts at the top.
- The first image found supplies the reference position for clicking.
- For Image found, no matching image means the condition's actions are skipped.
- Image not found is true only when none of the registered images is visible.

To edit the list:

1. Open an image condition. The image list is on the left and the preview is on the right.
2. Add a new capture, or select an already saved project image from Add existing image.
3. Select an item to preview it.
4. Double-click it or press Enter to recapture or crop it.
5. Rename changes the file name. Remove only removes the list entry. Delete to Recycle Bin removes the image file. Use Up and Down to change search order.

Confidence and search region apply to all images by default. Select an image to set its individual confidence or search region; otherwise it uses the shared values.

A successful search briefly outlines the match in red. Toggle this with Show search results in the upper toolbar.

> [!NOTE]
> A single registered image behaves as before. Existing macros remain usable.

![Image list and preview in the condition editor](../img/8.-이미지-검색과-캡처-02.png)

## Click relative to a found image

Click the found image itself or apply an offset. For example, find a checkbox label and offset the click to the checkbox.

To click a confirmation button whose position varies:

1. Capture its text or icon.
2. Add an image-relative click step.
3. Click the match center or adjust the offset.
4. If the image is visible, the click follows its position even after the window moves.

Image-relative clicks and moves require a successful preceding Image found search. Without a valid reference position, only that action is skipped and the macro continues. Place these actions inside **Image found**, not Image not found.

## Image filtering options

The Image filtering group in the capture/editor window sets per-image matching options. Open it by selecting an image and double-clicking or pressing Enter.

### Ignore color: grayscale

Enable Ignore color (grayscale) to convert both the screen and template to grayscale before comparison. This can help when:

- Light and dark themes change button colors.
- Night or high-contrast modes are used.
- Background colors change but shapes remain similar.

> [!TIP]
> Use Find on screen in the screen-search test area after enabling this option. Ignoring color can also produce false matches on similarly shaped elements.

### Ignore regions with a freehand mask

Paint over parts that change, such as numbers or status details, to exclude them from matching.

1. Double-click the image.
2. Select the Ignore-region pen in the top toolbar.
3. Drag with the left mouse button to paint ignored areas.
4. Use the right mouse button to erase.
5. Scroll up to enlarge the brush and down to shrink it, within `2 to 60 px`.
6. Use Clear mask to start over.

Masks are saved per image and do not affect others. Cropping preserves the mask within the cropped region. Masked images show a pen marker in the list.

> [!WARNING]
> Masking too much can cause false matches. Cover only the changing parts as narrowly as possible.

## Confidence

The confidence setting changes matching strictness. The default was adjusted in `v1.0.13` for more reliable results. Lower it slightly if matching fails too often; raise it if similar but incorrect images are matched.

## Multiple monitors

Image search can be used with dual monitors. Start with a small test macro to confirm matching on the intended screen.

## Adjust the capture region

![Capture region selection](../img/8.-이미지-검색과-캡처-01.png)

- **Move**: drag inside the selected region.
- **Resize**: move to an edge or corner until a directional cursor appears, then drag.
- **Zoom preview**: while adjusting the region, the upper-right popup shows an enlarged preview.

To edit a captured image again, select it in the image list and double-click or press Enter.

## Capture tips

- Avoid frequently changing backgrounds.
- Prefer distinctive text or an icon over a whole button.
- Resolution and scaling changes can alter image appearance.
- Images that are too small can cause false positives or missed matches.

## Related guides

- [Conditions](04-conditions.md): click only when an image is visible.
- [Recording and playback](03-recording-and-playback.md): add image-based actions to a recording.
- [App introduction and installation](../../README.en.md)
- [Full manual contents](00-contents.md)

## Continue reading

[Manual home](README.md) | [Contents](00-contents.md) | [Previous: 7](07-variables-and-calculations.md) | [Next: 9](09-options-and-hotkeys.md)
