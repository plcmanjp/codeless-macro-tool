# 12. Sample steps: start from built-in examples

[한국어](../12.%20%EC%83%98%ED%94%8C%20%EC%8A%A4%ED%85%9D.md) | **English**

[Manual home](README.md) | [Contents](00-contents.md) | [Previous: 11](11-regex-extraction.md) | [Next: 13](13-ocr.md)

Screenshots show the Korean interface; captions and instructions are in English.

## Sample steps

## What are sample steps?

Sample steps are the app's built-in, read-only examples. Insert common structures for copying, pasting, loops, conditions, variables, and comments to learn the macro-authoring workflow.

## Sample steps versus favorites

You cannot add, edit, or delete entries in the built-in sample collection. Favorites are your personal reusable steps. Since `v1.0.23`, new users no longer receive automatically created default favorites; built-in examples are provided through Sample steps instead.

## How to insert samples

1. Click Sample steps at the top of the main window.
2. Choose General, Mouse, Keyboard, Loops, Conditions, Variables, or Other.
3. Select an item and confirm, or double-click it.
4. The sample is inserted below the selected row.

With no row selected, it is appended to the end of the step list.

![Sample steps dialog](../img/12.-샘플-스텝-01.png)

## Categories

| Category | Examples |
| --- | --- |
| General | Copy, Paste, Select all, Save, Undo, 500 ms wait |
| Mouse | Movement, click preparation, and scrolling examples |
| Keyboard | Single keys, combinations, key down/up, text input with waits |
| Loops | Three-iteration block and multiplication-table example |
| Conditions | Image found/not found, A AND B, A OR B, A OR B ELSE, (A AND B) OR C, A ELSE IF B, A ELSE IF B ELSE, BREAK inside a loop |
| Variables | Counter variable |
| Other | Comment step |

## Examples

**Build a loop from a sample**

1. Choose Loops.
2. Insert the basic three-iteration block.
3. Put actual clicks, text input, or delays between Loop start and Loop end.
4. Adjust the count.

**Explore nested loops with the multiplication table**

1. Choose Loops.
2. Insert the multiplication-table example.
3. Focus a text input area such as Notepad.
4. Run it to output tables from 2 through 9 using the sample's X, Y, and result variables. The Korean sample displays the template `%X x %Y = %결과`.

**Create a counter**

1. Choose Variables.
2. Insert the counter sample.
3. Adjust its name and initial value.
4. Combine it with text input or calculations to enter a different value on each iteration.

**Create image branches**

1. Choose Conditions.
2. Select the appropriate example.

| Example | Use |
| --- | --- |
| Image found/not found | Run A when the image exists and B otherwise |
| A AND B | Run only when both images are visible |
| A OR B | Run shared actions when either image is visible |
| A OR B ELSE | Shared actions for either image, fallback when neither is visible |
| (A AND B) OR C | Run when both A and B are visible, or when C is visible |
| A ELSE IF B | Check B only if A is false |
| A ELSE IF B ELSE | Choose between A, B, and a fallback |

3. Double-click each image-condition step to set its reference image.
4. Add the actions inside the appropriate condition blocks.

For an AND chain, put actions **inside the last IF block**. Actions inside the first IF block are ignored.

**Build sequential branches with ELSE IF**

1. Choose Conditions.
2. Insert A ELSE IF B or A ELSE IF B ELSE.

| Example | Evaluation | Use |
| --- | --- | --- |
| A ELSE IF B | Run A if true; otherwise check B | Distinguish two states in order |
| A ELSE IF B ELSE | Check A, then B, then fallback | Success, warning, and other outcomes |

3. Configure the comparison images by double-clicking their steps.
4. Add each branch's actions.

ELSE IF checks the next condition only when preceding ones are false and gives each branch its own actions. OR runs **shared actions** if any condition is true. See [Conditions](04-conditions.md).

**Use BREAK inside a loop**

1. Choose Conditions.
2. Insert the BREAK-inside-a-loop sample.
3. Double-click the inner image condition and set the escape condition.
4. Add any actions needed before BREAK.

BREAK skips the remaining processing in the current iteration and continues with the next iteration. See [Conditional BREAK](04-conditions.md#break-escape-nested-if-blocks).

![Multiplication-table sample inserted in the step list](../img/12.-샘플-스텝-02.png)

## Notes

- The built-in collection is read-only.
- Samples cannot be inserted while playback is running.
- Once inserted, sample steps can be edited like ordinary steps.
- Mouse samples default to safe movement, comments, and waits rather than actual clicks.
- The multiplication-table example types text. Focus the intended output field before running it.
- Existing favorites in `favorites.json` are preserved.

## Related guides

- [Conditions](04-conditions.md)
- [Favorites](10-favorites.md)
- [App introduction and installation](../../README.en.md)
- [Full manual contents](00-contents.md)

## Continue reading

[Manual home](README.md) | [Contents](00-contents.md) | [Previous: 11](11-regex-extraction.md) | [Next: 13](13-ocr.md)
