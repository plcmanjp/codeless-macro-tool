# 4. Conditions: branch according to the situation

[한국어](../4.%20%EC%A1%B0%EA%B1%B4.md) | **English**

[Manual home](README.md) | [Contents](00-contents.md) | [Previous: 3](03-recording-and-playback.md) | [Next: 5](05-loops.md)

Screenshots show the Korean interface; captions and instructions are in English.

## Conditions

## What is a condition step?

A condition step runs the steps inside it only in a particular situation. When the screen state varies, conditions make a macro more reliable than an unconditional sequence of clicks.

## Supported conditions

| Condition | Example |
| --- | --- |
| Pixel color matches | Run only when a status light is green |
| Image found | Continue when a save-complete message appears |
| Image not found | Continue when a loading icon disappears |
| Key is pressed | Run a branch while a particular key is held |
| Variable comparison | Choose actions based on copied text or a calculation |
| Always true | Always run this branch |
| Always false | Always skip this branch, useful for temporarily disabling it |

## Example 1: close an error popup only when it appears

1. Capture the popup's title or close-button image.
2. Add Condition start.
3. Select Image found.
4. Add the close-button click inside the condition.
5. Add Condition end.

If the popup is absent, the click is skipped.

## Example 2: continue after a loading icon disappears

1. Capture the loading icon.
2. Add Condition start.
3. Select Image not found.
4. Put the next-button click or text input inside the condition.
5. If necessary, add a short delay beforehand to allow the screen to update.

This bases the next action on the screen state instead of relying only on a fixed wait.

## Example 3: run only for a specific variable value

1. Store the value with variable assignment or regular expression extraction.
2. Add Condition start.
3. Select Variable comparison.
4. Enter the variable, comparison operator, and comparison value.
5. Add the required steps inside the condition.

The comparison value can be a number, ordinary text, or `%variableName`. Typing `%` opens the variable picker if variables exist. For example, click Save only when `Result` equals `Success`.

## Example 4: run while a particular key is held

1. Add Condition start.
2. Select Key is pressed.
3. Choose the key.
4. Add the actions inside the condition.

This is useful for temporarily enabling a particular action while testing.

## Branch types at a glance

Condition start alone gives a true/false choice. The branch steps provide more options:

| Step | Purpose |
| --- | --- |
| AND | All joined conditions must be true to run the shared branch |
| OR | Any joined condition can be true to run the shared steps |
| ELSE IF | Evaluate a new condition when preceding branches are false |
| ELSE | Run when all preceding conditions are false |
| IF_END | Close the entire chain once, rather than closing each branch separately |
| IF_BREAK | Escape enclosing conditional blocks |

Choose AND, OR, ELSE IF, or ELSE from the **Condition logic** submenu. Double-click a connector in the step list to change its type, for example OR to ELSE IF or ELSE IF to ELSE.

**Add branches within individual clauses**

For a chain such as `IF → ELSE IF → ELSE IF`, place the cursor inside the relevant clause to add a connector there.

- Inside an ELSE IF clause, choose Condition logic → AND to add another condition to that clause.
- You can add a following ELSE IF or ELSE from inside an ELSE IF clause.
- ELSE can only be added to the **last clause**. If an ELSE already exists, its menu item is disabled.

> [!TIP]
> Select the relevant clause to extend a complex chain. You do not need to delete and rebuild the whole chain.

![Indented condition branches in the step list](../img/4.-조건-01.png)

## OR: run shared steps when any condition is true

OR combines conditions for **shared actions**. AND requires all conditions to be true; OR requires at least one.

1. Add Condition start and configure the first condition.
2. Below it, choose Condition logic → OR.
3. Configure the second condition step added automatically after OR.
4. Put the shared actions inside the final condition step.
5. Close the chain with Condition end.

Evaluation proceeds in order. If the first condition is true, run the shared steps. Otherwise evaluate the second. Once any condition is true, run the shared steps and skip the remaining conditions. If all are false, skip the shared steps.

```text
IF image A is found
OR image B is found
OR image C is found
  Click: run if any of A, B, or C is found
END IF
```

> [!TIP]
> Use **ELSE IF** when each condition needs different actions. OR conditions share the same actions.

> [!NOTE]
> Opening OR macros created in `v1.0.38` or earlier may show a behavior-change notice. If your old macro uses different actions for each OR branch, change those branches to ELSE IF.

## ELSE IF: try another condition when earlier branches are false

ELSE IF starts a new branch with its own condition. Build multiple branches as `IF → ELSE IF → ELSE IF → ELSE`.

1. Add Condition start and configure the first condition.
2. Choose Condition logic → ELSE IF beneath the initial condition or the previous branch.
3. Configure the new condition. It can use a different type, such as an image, variable comparison, or color.
4. Add more ELSE IF branches as needed.
5. Add ELSE if a fallback action is needed.
6. Close the entire chain with Condition end.

If the initial IF is true, only its actions run. Otherwise the ELSE IF conditions are evaluated in order. The first true branch runs and the rest are skipped. If none is true, ELSE runs; without ELSE, no branch runs.

```text
IF state A
  Actions for A
ELSE IF state B
  Actions for B
ELSE IF state C
  Actions for C
ELSE
  Fallback actions
END IF
```

OR is concise when several similar conditions lead to the same actions, such as any of several images being visible. ELSE IF is suitable when different states or condition types need separate actions, such as an image test followed by a variable comparison and then a color test.

## ELSE: run when all conditions are false

1. Choose Condition logic → ELSE below an IF, OR, or ELSE IF clause.
2. Add the actions to run when all conditions are false.
3. Close the entire chain with Condition end.

```text
IF image A is found
OR image B is found
  Shared actions when A or B is found
ELSE
  Actions when neither image is found
END IF
```

## AND: require multiple conditions together

AND runs the branch only if both the previous and the following conditions are true. Any false condition prevents the branch from running.

Select Condition start or place the cursor inside the condition block and choose Condition logic → AND. The following Condition start becomes the second condition.

```text
IF image A is found
AND
  IF variable equals Done
    Actions requiring both conditions
END IF
```

Put actions **inside the last Condition start block**. Actions placed in the first block do not run. For example, join the image test and `Status == Done` with AND.

When an AND group performs multiple image searches, the app hides and restores its window once per group to reduce flicker.

## Example 5: click different buttons for different images

Use separate branches when different popups need different buttons:

1. Capture a distinctive part of each popup.
2. Add Condition start with Image found for the first image.
3. Put the first popup's button click inside that branch.
4. Add ELSE IF with Image found for the second image.
5. Put the second popup's button click inside that branch.
6. Optionally add ELSE for the case where neither popup is present.
7. Add Condition end.

This adapts the actions to the popup that actually appears.

## Example 6: different actions for different states

Use an ELSE IF chain for four outcomes:

- `Result == Success`: click Save.
- `Result == Warning`: close the confirmation dialog.
- `Result == Error`: click Retry.
- Any other value: perform your finish actions.

1. Prepare `Result` with regular expression extraction or variable assignment.
2. Set Condition start to `Result == Success`.
3. Add ELSE IF for `Result == Warning`.
4. Add ELSE IF for `Result == Error`.
5. Add ELSE and the finish actions.
6. Add Condition end.

```text
IF Result == Success
  Click Save
ELSE IF Result == Warning
  Close confirmation dialog
ELSE IF Result == Error
  Click Retry
ELSE
  Finish actions
END IF
```

## Example 7: combine image AND conditions with ELSE IF

Click A if image A is visible and `Status` is `Running`. Otherwise click B if image B is visible. Do nothing if neither case applies.

1. Set Condition start to Image A found.
2. Add AND and a new Condition start for `Status == Running`.
3. Put the click on A inside the final condition.
4. Add ELSE IF for Image B found.
5. Put the click on B inside that branch.
6. Close with Condition end.

```text
IF image A is found
AND
  IF Status == Running
    Click A
ELSE IF image B is found
  Click B
END IF
```

## Example 8: branch inside a loop

Run ten iterations, performing action A on even iterations and action B on odd iterations.

1. Assign `Iteration = 1` and disable reset on repeat.
2. Add Loop start with a count of `10`.
3. Calculate `EvenCheck = Iteration % 2`.
4. Add a condition for `EvenCheck == 0`, with action A inside.
5. Add ELSE with action B.
6. Add Condition end.
7. Increment `Iteration`.
8. Add Loop end.

```text
Set Iteration = 1, reset on repeat off
LOOP 10 times
  Calculate EvenCheck = Iteration % 2
  IF EvenCheck == 0
    Action A
  ELSE
    Action B
  END IF
  Increment Iteration
END LOOP
```

## Missing paths or files in image conditions

If an Image found or Image not found condition has an empty path or a missing file, the runtime skips the **entire condition block**, from Condition start through Condition end, including ELSE IF and ELSE. It does not treat this as an ordinary false result. Execution continues after Condition end without running any branch.

This prevents a macro saved without its captured image from taking unintended actions.

For pixel-color, variable-comparison, and key-pressed conditions, missing input instead evaluates as false, so an ELSE branch can run.

| Condition | Behavior with missing input |
| --- | --- |
| Image found / Image not found | Skip the entire block, including ELSE |
| Pixel color / Variable comparison / Key pressed | Evaluate as false; ELSE can run |

Check image files in the editor before playback. Pre-run validation may report missing images before runtime begins.

## BREAK: escape nested IF blocks

Conditional BREAK escapes enclosing IF blocks when further conditional processing should stop.

**Rules**

- The nearest LOOP boundary absorbs BREAK. The current iteration ends, but the next iteration continues.
- A POINTER boundary also absorbs BREAK. A BREAK inside a pointer ends that pointer and resumes after its call. It does not affect IF blocks in the caller.
- Outside an IF block, BREAK has no effect.

**Add BREAK**

Place the cursor inside a condition block and choose Condition logic → BREAK. The menu item is disabled outside a condition block.

**Example 1: skip the rest of the current iteration**

```text
LOOP 10 times
  IF error image is found
    Handle error
    BREAK
  END IF
  Next click: reached only when BREAK did not occur
END LOOP
```

When the image is found and BREAK runs, the rest of that iteration is skipped and the next iteration starts.

**Example 2: escape nested conditions at once**

```text
IF state A
  IF subcondition B
    Process
    BREAK: leave both B and A
  END IF
  Not executed
END IF
Not executed: the top-level safety boundary absorbs BREAK
```

BREAK leaves enclosing condition blocks until the nearest loop or pointer boundary. At the top level, the safety boundary absorbs it.

## Authoring tips

- Keep only necessary steps inside a condition.
- Check what happens when a condition fails.
- Capture small, distinctive image regions for more reliable matching.
- Use the variable monitor to inspect actual values while configuring comparisons.
- AND, OR, ELSE IF, and ELSE appear at the same indentation level as Condition start.
- Close each condition chain with exactly one Condition end.
- Use ELSE IF for separate branches; OR is shorter for multiple image tests sharing actions.
- Double-click connectors to change their type, such as OR ↔ ELSE IF or ELSE IF ↔ ELSE.
- Older macros containing ELSE are converted to the new structure when opened and can then be edited normally.

## Pre-run condition structure checks

Before playback, the app checks condition boundaries and the order of AND, OR, ELSE IF, and ELSE. A connector without Condition start, AND/OR after the chain has ended, or duplicate ELSE branches produces an error with a location and correction guidance. Input does not begin.

Go to the indicated step, fix matching boundaries, and place shared actions inside the final condition branch before trying again.

## Related guides

- [Image search and capture](08-image-search-and-capture.md)
- [Pointers](06-pointers.md): reuse shared conditional handling.
- [App introduction and installation](../../README.en.md)
- [Full manual contents](00-contents.md)

## Continue reading

[Manual home](README.md) | [Contents](00-contents.md) | [Previous: 3](03-recording-and-playback.md) | [Next: 5](05-loops.md)
