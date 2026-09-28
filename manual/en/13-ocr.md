# 13. OCR: read on-screen text into a variable

[한국어](../13.%20OCR%20%ED%85%8D%EC%8A%A4%ED%8A%B8%20%EC%9D%BD%EA%B8%B0.md) | **English**

[Manual home](README.md) | [Contents](00-contents.md) | [Previous: 12](12-sample-steps.md) | [Next: 14](14-background-input.md)

Screenshots show the Korean interface; captions and instructions are in English.

## OCR text reading

## What is OCR text reading?

OCR recognizes text in a screen region. Save the result in a variable or test whether it contains a keyword. Use stock counts, status messages, or button labels as input to later actions.

Examples include reading stock and clicking Order when it is zero, continuing when a completion message appears, retrying when error text appears, or clicking a recognized word.

## Before using OCR: the ko-KR language pack

The app uses Windows' built-in WinRT `Windows.Media.Ocr` engine. Its OCR feature requires the **Korean (ko-KR) language pack**. Without it, OCR steps and conditions are disabled and the editor shows installation guidance.

### Install the ko-KR language pack

1. Open Windows Settings from Start or with `Win+I`.
2. Select **Time & language → Language & region**.
3. Click **Add a language**.
4. Search for Korean and select **Korean (South Korea)**.
5. Install the language pack or basic typing feature offered in the installation options.
6. Restart JP's Codeless Macro Tool.

> [!NOTE]
> On English Windows, adding the Korean language pack enables the app's OCR feature. You do not need to change the Windows display language.

## OCR_READ: save screen text to a variable

An OCR text reading step captures a region, recognizes its text, and stores the result in a chosen variable.

### When to use it

- Read a displayed number or status for later steps.
- Extract a specific value by following OCR with regular expression extraction.
- Click relative to a recognized word.

### Add the step

1. Select the desired position in the step list.
2. Choose OCR text reading from the add-step menu.
3. Configure the editor that opens.

![OCR text-reading step editor](../img/13.-OCR-텍스트-읽기-01.png)

### Fields

| Field | Description |
| --- | --- |
| Reading region (ROI) | Drag to choose the screen area; without a region, the whole screen is used |
| Destination variable | Choose an existing variable or enter a new name |
| Save text position | Store the screen position of the first recognized word for a later mouse action |
| Test / Read | Recognize the current screen immediately and preview the result before saving |

### Select an ROI

1. Click Select region to enter screen-capture mode.
2. Drag around the text.
3. Keep the region close to the intended text to avoid unrelated content.
4. After selection, return to the editor.

![Selecting an OCR region by dragging](../img/13.-OCR-텍스트-읽기-05.png)

### OCR preview

Click Test / Read to open the preview window.

![OCR preview window](../img/13.-OCR-텍스트-읽기-02.png)

| Control | Description |
| --- | --- |
| Upscale factor | Enlarge the image before recognition, with factors from 2 to 5 for small fonts or low-resolution screens |
| Automatic binarization (Otsu) | Determine the black/white threshold automatically; suitable for most cases |
| Manual binarization | Adjust the brightness threshold with a slider for low-contrast text |
| Preview | Inspect the processed image and recognized text; red boxes mark word positions |

> [!TIP]
> Try an upscale factor of at least 2 for small text or numbers. Larger factors can increase processing time.

### Example: read a stock count

1. Add an OCR text-reading step.
2. Set the ROI to the stock-count area.
3. Enter `StockCount` as the destination variable.
4. Test the current screen and check the result.
5. Save the step.

After playback, inspect `StockCount` in the variable monitor. Its value is the recognized number as text.

## text_contains: branch when text contains a keyword

The Screen text contains condition tests OCR text from a region for a keyword.

### When to use it

- Continue when a status such as Complete or Error appears.
- Choose another action when a particular word is absent.

### Add the condition

1. Select the insertion position.
2. Add Condition start.
3. Select Screen text contains.
4. Set the ROI and keyword.

![Screen text contains condition editor](../img/13.-OCR-텍스트-읽기-03.png)

### Fields

| Field | Description |
| --- | --- |
| Reading region (ROI) | The screen area to recognize |
| Keyword | The word or string to look for |
| Does not contain | Make the condition true when the keyword is absent |
| Test | Recognize the current screen and check the keyword immediately |

### Example: continue on completion

```text
IF screen text contains "Complete"
  Click Next
END IF
```

1. Add Condition start with Screen text contains.
2. Select the status-message region.
3. Enter `Complete` as the keyword.
4. Put the Next-button click inside the condition.
5. Add Condition end.

### Example: save only when no error text appears

```text
IF screen text does not contain "Error"
  Click Save
END IF
```

Enter `Error` and enable Does not contain.

> [!NOTE]
> This tests **substring inclusion**, not exact equality. A message such as `Processing Complete` also contains `Complete`. Use keywords matching the actual language shown by the target application.

## use_text_pos: click a recognized word

Mouse steps can use the screen position produced by OCR.

### When to use it

- A button label or item appears in varying positions.
- You need to click text without relying on a fixed coordinate.

### Steps

1. Enable Save text position in an OCR text-reading step.
2. Add a following mouse action such as click or move.
3. Enable Use text OCR position in the mouse editor.
4. During playback, the action uses the center of the first recognized word.

![Use text OCR position in a mouse step](../img/13.-OCR-텍스트-읽기-04.png)

### Example

```text
OCR read: selected ROI, variable ResultText, save text position on
Mouse click: use text OCR position on
```

> [!NOTE]
> The preceding OCR read must succeed and provide a word position. Otherwise that mouse step is skipped and the macro continues.

This works like image-relative clicking with `use_image_pos`. Both options can be configured, but text position takes priority when enabled.

## Extract numbers with OCR_READ and regular expressions

### Situation

A stock screen shows `Current stock: 42 items`. Extract only `42` and use it in a condition.

### Steps

```text
OCR read: stock display ROI, variable StockText
Regex extraction: source StockText, pattern \d+, destination StockCount
IF StockCount == 0
  Click Order
END IF
```

1. Read the message into `StockText`.
2. Extract one or more digits with `\d+` into `StockCount`.
3. Click Order when the variable comparison finds zero.

See [Regular expression extraction](11-regex-extraction.md).

## Notes

### Avoid exact text comparisons

Fonts, resolution, and screen state can change OCR output. For example, punctuation may be included unexpectedly. The OCR condition therefore tests substring inclusion rather than exact equality.

An exact variable comparison such as `Result == "Processing Complete"` can fail on a small recognition difference. Prefer Screen text contains or extraction followed by further processing.

### Very short words may be unreliable

Korean words of two characters or fewer can be recognized inconsistently. Prefer specific keywords of at least three characters when possible, such as the Korean phrases for processing complete or in progress.

### Upscale small fonts

Small fonts and low-resolution screens can reduce accuracy. Check the preview and try an upscale factor of at least 2.

### Keep the ROI narrow

A wide region can include unrelated text. Select only the text you need.

### Missing ko-KR disables the feature

If OCR steps and conditions are greyed out because the required pack is missing, follow the installation instructions above.

## Related guides

- [Regular expression extraction](11-regex-extraction.md)
- [Image search and capture](08-image-search-and-capture.md)
- [Conditions](04-conditions.md)
- [Variables and calculations](07-variables-and-calculations.md)
- [App introduction and installation](../../README.en.md)
- [Full manual contents](00-contents.md)

## Continue reading

[Manual home](README.md) | [Contents](00-contents.md) | [Previous: 12](12-sample-steps.md) | [Next: 14](14-background-input.md)
