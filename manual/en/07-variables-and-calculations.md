# 7. Variables and calculations

[한국어](../7.%20%EB%B3%80%EC%88%98%EC%99%80%20%EC%97%B0%EC%82%B0.md) | **English**

[Manual home](README.md) | [Contents](00-contents.md) | [Previous: 6](06-pointers.md) | [Next: 8](08-image-search-and-capture.md)

Screenshots show the Korean interface; captions and instructions are in English.

## What is a variable?

Variables store values for reuse while a macro runs. Increment a number between repetitions, change part of some text, or use a calculation result in another step. Regular expression extraction can also save selected parts of a string into another variable.

## Variable assignment

Configure a name, initial value, and format in a variable assignment step.

| Field | Description |
| --- | --- |
| Variable name | Reference this name as `%variableName` in text or formulas |
| Initial value | The first value used when the macro starts |
| Type / format | How values are interpreted and displayed |
| Candidate values | Choices for a selection variable |
| Reset on repeat | Whether the variable returns to its initial value on each repetition |

### Types and formats

| Type | Meaning | Example |
| --- | --- | --- |
| Decimal | Ordinary number | `42` |
| Hexadecimal | Base-16 number | `2A` |
| Octal | Base-8 number | `52` |
| Text | Literal text without numeric calculation | `Apple` |
| Clipboard | Read the system clipboard at runtime | - |

Numeric types can be used in calculation steps. Text variables can be substituted in text input, but cannot be used as numeric operands in calculation formulas.

![Variable assignment editor](../img/7.-변수와-연산-01.png)

## Selection variables with dropdowns

> [!TIP]
> Since `v1.0.49`, candidate values let you change a variable through a dropdown in the main window without opening its editor.

Enter comma-separated candidates to create a selection variable:

- Text: `A, B, C`
- Decimal numbers: `10, 20, 30`
- Hexadecimal numbers: `0A, 1F, FF`

A dropdown appears in the variable's row. Select a value and playback uses it.

### Behavior by candidate type

| Candidates | Calculations | Text input |
| --- | --- | --- |
| Valid numbers in the declared format | Supported | Supported |
| Candidates containing nonnumeric text | Calculation is skipped | Supported |

For a hexadecimal variable, `0A, 1F, FF` are numeric candidates. If candidates contain ordinary nonnumeric text, they are treated as text candidates. A calculation referencing a text-candidate variable is skipped, but text input can still use it.

### Example

To select a server, region, or department without reopening the editor:

1. Create a Text variable named `Environment` with candidates `Development, Test, Production`.
2. Find its dropdown in the main window.
3. Select `Test`; a text input step referencing the variable will enter `Test`.

![Selection-variable dropdown in the step table](../img/7.-변수와-연산-02.png)

## Reset on repeat

When enabled, the variable returns to its initial value each time a repetition starts. When disabled, it retains changes from the previous repetition. Disable it for a counter that should keep increasing; enable it when every repetition should start from the same value.

## Store clipboard content in a variable

Choose Clipboard as the assignment type to read clipboard content at runtime. After copying text with `Ctrl+C`, wait for the clipboard change before storing it.

1. Add keyboard action `ctrl+c`.
2. Add a delay using Wait for clipboard change.
3. Add a variable assignment named `Copied`, with type Clipboard.

> [!WARNING]
> `ctrl+c → variable assignment → clipboard wait` can store the previous clipboard value. Use `ctrl+c → clipboard wait → variable assignment` in that order.

## Use variables in text input

Typing `%` in a text input field opens a picker for available variables.

```text
Item%N
```

If `N` is `001`, this enters `Item001`.

To generate numbered item names:

1. Declare decimal variable `N` with initial value `001`.
2. Enter `Item-%N` in a text input step.
3. Increment `N` by 1 after the input.
4. Repeated playback enters `Item-001`, `Item-002`, `Item-003`, and so on.

Longer variable names are matched first. If both `OrderNumber` and `Order` exist, `%OrderNumber` substitutes the complete `OrderNumber` variable.

## Variable replacement

A replacement step finds text in a source string and substitutes other text. Choose separate source and destination variables to preserve the original, or the same variable to overwrite it. Clipboard can be either source or destination.

One step can contain several replacement rules.

| Item | Description |
| --- | --- |
| Search text | Text to find; it cannot be empty when saving |
| Replacement text | Text to insert; leave empty to delete matches |
| Order | Apply rows from top to bottom |
| Row controls | Add replacement, Delete, Up, and Down |
| Shortcuts | Alt+Up/Down moves selected rows; Delete removes them |

Search and replacement fields accept ordinary text and `%variableName`. Typing `%` opens the picker when variables exist; otherwise it remains a literal character.

Example: clean copied text in one step.

| Order | Search | Replace with |
| --- | --- | --- |
| 1 | A space | `_` |
| 2 | `OrderNumber:` | `ORDER=` |
| 3 | `%RemoveText` | Empty |

This replaces spaces with underscores, changes the label to `ORDER=`, then removes the text stored in `RemoveText`.

To replace spaces in clipboard text:

1. Run `ctrl+c`.
2. Wait for a clipboard change.
3. Choose Clipboard as the replacement source.
4. Enter a space as Search text and `_` as Replacement text.
5. Choose Clipboard as the destination.

Source and destination are always selected from dropdowns. Clipboard is available even with no declared variables. Neither field has a default selection.

## Variable calculations

Calculation steps can increment or decrement numbers, perform arithmetic, modulo or powers, store results in another variable, or copy results to the clipboard. Typing `%` in a formula opens the variable picker, for example to build `%COUNT + 1`.

### Operators

| Operator | Meaning | Example |
| --- | --- | --- |
| `+` `-` `*` `/` | Arithmetic | `%N + 1` |
| `//` | Integer division | `%N // 3` |
| `%` | Remainder | `%N % 10` |
| `**` | Power | `%N ** 2` |
| `++` | Increment destination by one | `++` |
| `--` | Decrement destination by one | `--` |

Enter `++` or `--` directly in the formula field to change the destination variable by one. Mathematical functions such as `sin`, `cos`, `sqrt`, and `abs` are also available.

> **Hexadecimal values in formulas**
> When substituting `%variable`, a value string with a `0x` prefix is interpreted as hexadecimal; without that prefix, it is interpreted as decimal. Values filled by OCR or regular expression extraction therefore need a `0x` prefix if you intend hexadecimal calculation. A read value of `10` means decimal 10; `0x10` means decimal 16. Keep the prefix on values intended as hexadecimal.

### Result destination

- **Variable**: store the result in a selected variable and view it in the variable monitor.
- **Clipboard**: copy the result to the system clipboard. It is not stored as variable state and does not appear in the variable monitor.

No destination is selected by default. An empty destination produces a warning and blocks saving.

### Result format

Results follow the destination variable's declared format. If `CODE` is hexadecimal, its result is displayed in hexadecimal. The calculation step does not independently select a display format. Clipboard results are always copied in decimal.

To paste a calculation result immediately:

1. Store the current number in `COUNT`.
2. Enter `%COUNT + 1` as the formula.
3. Select Clipboard as the result destination.
4. Run `ctrl+v` in the next step.

> [!NOTE]
> Text variables and selection variables with text candidates cannot be used in numeric formulas. A calculation referencing one is skipped, and the log monitor explains why.

![Variable calculation editor](../img/7.-변수와-연산-03.png)

## Variable monitor

The monitor displays values as they change during execution. Use it to investigate unexpected values, calculation results, or extraction results.

### Edit directly from the monitor (v1.0.49)

| Double-click location | Editor opened |
| --- | --- |
| Name or value column | Variable assignment: initial value, type, candidates, and related settings |
| Description column | Calculation or regular expression extraction |

Save an edited operation or extraction step to apply it to the macro immediately.

### Live updates (v1.0.49)

Adding, deleting, or editing variables immediately refreshes the monitor list and descriptions. Dropdown selections are also reflected immediately. Descriptions show selected values, initial values, and formulas.

![Variable monitor](../img/7.-변수와-연산-04.png)

## Regular expression extraction

Extract a required part of a source string into another variable. For example, extract the order number or amount from `Order: A-1024 / Amount: 35000` for later steps. See the examples in [Regular expression extraction](11-regex-extraction.md).

## The %variableName picker

When variables are declared, typing `%` offers a picker in these fields:

| Field | Example |
| --- | --- |
| Text input | `Order: %OrderNumber` |
| Replacement search and replacement text | Find `%RemoveText` and replace it with empty text |
| Calculation formula | `%COUNT + 1` |
| IF variable-comparison value | Compare against `%Threshold` |
| Extraction source and destination fields | Assist entry of `%SourceText` and `%Extracted` |

Without declared variables, no picker appears and `%` remains as typed. You can also type it as ordinary text.

## Common mistakes

- **Reading the clipboard too soon**: insert Wait for clipboard change between `ctrl+c` and clipboard-variable assignment.
- **Using text in arithmetic**: use a numeric type when calculation is required. Text-candidate variables also cannot be calculated.
- **Resetting a counter**: turn reset on repeat off to accumulate values across repetitions.
- **Expecting a calculation step to change display format**: the destination variable's declaration determines the result format.

## Related guides

- [Regular expression extraction](11-regex-extraction.md)
- [Loops](05-loops.md)
- [Conditions](04-conditions.md)
- [App introduction and installation](../../README.en.md)
- [Full manual contents](00-contents.md)

## Continue reading

[Manual home](README.md) | [Contents](00-contents.md) | [Previous: 6](06-pointers.md) | [Next: 8](08-image-search-and-capture.md)
