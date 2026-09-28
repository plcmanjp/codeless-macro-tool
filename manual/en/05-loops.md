# 5. Loops: click coordinates in sequence

[한국어](../5.%20%EB%B0%98%EB%B3%B5.md) | **English**

[Manual home](README.md) | [Contents](00-contents.md) | [Previous: 4](04-conditions.md) | [Next: 6](06-pointers.md)

Screenshots show the Korean interface; captions and instructions are in English.

## Loops

## What is a loop step?

A loop repeats a group of steps a chosen number of times. Use it to click the same button repeatedly, repeat a procedure, or process many items while changing a variable.

## Basic structure

Loop start and Loop end form a pair:

```text
LOOP
  Steps to repeat
END LOOP
```

Enter the repetition count in Loop start.

## Example 1: click a button five times

1. Add Loop start with count `5`.
2. Put a Mouse click step inside it.
3. Add a short delay after the click if needed.
4. Add Loop end.

## Example 2: use a variable in a loop

A changing variable produces different output on each iteration.

1. Create `N` with initial value `001`.
2. Add Loop start.
3. Add text input using `N`.
4. Increment `N` by 1 with a calculation step.
5. Add Loop end.

See [Variables and calculations](07-variables-and-calculations.md) for declaration and substitution syntax.

## Example 3: nested loops

You can put a loop inside another loop. For example, an outer loop selects rows and an inner loop selects columns. Test with small counts before increasing them.

## Example 4: coordinate arrays

When a mouse step has a coordinate array, loop iterations use the coordinates in order. A single coordinate is reused every time. With multiple coordinates, the first iteration uses the first coordinate, the second uses the second, and so on. When iterations outnumber coordinates, the array cycles from its beginning.

### Coordinate editor

The mouse-step editor starts with one coordinate row. Add rows to create an array.

| Control | Function |
| --- | --- |
| Capture (F2) | Capture a screen coordinate. Use the capture countdown or press F2 for immediate capture |
| Add row (F3) | The button duplicates the selected coordinate; F3 appends the current cursor position |
| Delete (Del) | Remove selected rows, including multiple rows at once |
| Delete all | Clear all coordinate rows |
| Up (Alt+↑) / Down (Alt+↓) | Reorder rows; multiple selected rows move as a block |
| Auto-generate | Generate a grid from a base coordinate and pitch |

**Select multiple rows**

| Method | Result |
| --- | --- |
| Ctrl+A | Select all rows |
| Shift+click | Select a continuous range from the initially selected row |
| Ctrl+click | Add individual nonadjacent rows |
| Shift+↑↓ | Extend the selection with the keyboard |

**Coordinate preview**

Enable Coordinate preview above the table to show numbered points on the screen in real time. This helps check positions while editing.

![Coordinate table and preview](../img/5.-반복-01.png)

### Generate a coordinate grid

Click Auto-generate above the table to create a grid in one operation.

- **Base coordinate**: the starting point, captured on screen or entered numerically.
- **X count / Y count**: numbers of columns and rows. Disabling one direction produces a single line.
- **X pitch / Y pitch**: spacing in pixels. Negative pitch reverses direction; negative X pitch extends to the left.
- **Fill order**: row-first fills across (`1 2 3 / 4 5 6 / 7 8 9`); column-first fills down (`1 4 7 / 2 5 8 / 3 6 9`).
- **Generation mode**: Zigzag is the default and fills each row in the same direction. Snake reverses even rows for a back-and-forth route. For a one-dimensional array, both modes behave the same.

**Calculate pitch with the mouse (F3)**: choose an endpoint on screen to calculate pitch from the distance to the base coordinate and the specified count. F3 starts immediately; clicking the button keeps the three-second countdown.

You can generate up to **2,000 coordinates**. Changes in the generator appear as a live grid preview before you apply them.

![Coordinate grid generator](../img/5.-반복-02.png)

Example: create a 5-column, 3-row grid with 80-pixel spacing.

1. Click Auto-generate.
2. Set the base coordinate to the first position at the upper left.
3. Enter X count `5` and Y count `3`.
4. Enter X pitch `80` and Y pitch `80`.
5. Choose row-first order.
6. Check the preview and confirm.
7. The table receives 15 coordinates.

Set a loop count of 15 to click each position in order.

![Loop containing a mouse click coordinate array](../img/5.-반복-03.png)

## Variable reset behavior

Variable assignment steps have a reset-on-repeat option:

- Enabled: return to the initial value on each repetition.
- Disabled: retain the value changed in the previous repetition.

> [!TIP]
> A continuously increasing counter usually needs reset on repeat disabled.

See [Variables and calculations](07-variables-and-calculations.md).

## Related guides

- [Pointers](06-pointers.md): reuse a procedure inside loops.
- [Variables and calculations](07-variables-and-calculations.md): vary values between iterations.
- [App introduction and installation](../../README.en.md)
- [Full manual contents](00-contents.md)

## Continue reading

[Manual home](README.md) | [Contents](00-contents.md) | [Previous: 4](04-conditions.md) | [Next: 6](06-pointers.md)
