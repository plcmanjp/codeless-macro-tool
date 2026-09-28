# 11. Regular expression extraction

[한국어](../11.%20%EC%A0%95%EA%B7%9C%EC%8B%9D%20%EC%B6%94%EC%B6%9C.md) | **English**

[Manual home](README.md) | [Contents](00-contents.md) | [Previous: 10](10-favorites.md) | [Next: 12](12-sample-steps.md)

Screenshots show the Korean interface; captions and instructions are in English.

## Regular expression extraction

## What is extraction?

Extract only the required part of a longer string and store it in a variable. For example:

```text
Order: A-1024 / Amount: 35000 won
```

Extract `A-1024` into `OrderNumber` for later text input, comparisons, or calculations when the value is numeric.

## When to use it

- Order, application, and transaction numbers
- Amounts, quantities, and dates
- Error codes in logs
- Numbers in file names or titles
- Parts of clipboard text or strings saved by earlier steps

If regular expressions are new to you, start by matching the fixed text before and after the value you want.

## Basic workflow

1. Store the source string in a variable.
2. Add a regular expression extraction step.
3. Enter the source variable name.
4. Enter the pattern.
5. Enter the destination variable name.
6. Check the test result before saving.

The source and destination fields accept names and `%variableName` input. Typing `%` opens a picker when variables are declared. The picker assists entry without forcibly rewriting text you typed yourself.

![Regular expression extraction editor](../img/11.-정규식-추출-01.png)

## A simple example

Suppose `Sentence` contains:

```text
Order: A-1024 / Amount: 35000 won
```

| Field | Value |
| --- | --- |
| Source variable | `Sentence` |
| Pattern | `Order:\s*([A-Z]-\d+)` |
| Destination variable | `OrderNumber` |

The resulting `OrderNumber` value is `A-1024`.

## Why parentheses matter

Parentheses `()` capture the part to save.

Pattern:

```text
Amount:\s*(\d+) won
```

Source:

```text
Amount: 35000 won
```

Result:

```text
35000
```

Without a capture group, the entire match is saved. For example, `Amount:\s*\d+ won` saves `Amount: 35000 won`.

## Common patterns

| Value | Pattern | Meaning |
| --- | --- | --- |
| Digits | `(\d+)` | One or more digits |
| Latin letters | `([A-Za-z]+)` | One or more letters |
| Korean syllables | `([가-힣]+)` | One or more Korean syllables |
| Optional whitespace | `\s*` | Zero or more whitespace characters |
| Any characters | `(.+)` | Broad match up to a line break |
| Date | `(\d{4}-\d{2}-\d{2})` | A date such as `2026-05-14` |
| Code | `([A-Z]-\d+)` | A code such as `A-1024` |

## Example 1: amount

Source:

```text
Payment: 48,500 won
```

Pattern:

```text
Payment:\s*([\d,]+) won
```

Result: `48,500`

## Example 2: date

Source:

```text
Processed: 2026-05-14 Complete
```

Pattern:

```text
Processed:\s*(\d{4}-\d{2}-\d{2})
```

Result: `2026-05-14`

## Example 3: error code

Source:

```text
ERROR [E-403] Permission denied.
```

Pattern:

```text
\[([A-Z]-\d+)\]
```

Result: `E-403`

Escape literal square brackets with a backslash, as in `\[` and `\]`.

## Example 4: number in a file name

Source:

```text
report_2026_001.xlsx
```

Pattern:

```text
report_\d+_(\d+)\.xlsx
```

Result: `001`

A dot has a special meaning in regular expressions. Use `\.` for a literal dot.

## Example 5: phone number copied to the clipboard

Suppose you copied this line from a webpage or message:

```text
Contact: Alex / Phone: 010-1234-5678 / Region: Seoul
```

Pattern:

```text
Phone:\s*(\d{3}-\d{4}-\d{4})
```

Result: `010-1234-5678`

Use fixed counts such as `\d{3}` when the number of digits is known.

## Example 6: date and time together

Source:

```text
Appointment: 2026-05-16 14:30 / Status: Confirmed
```

Pattern:

```text
Appointment:\s*(\d{4}-\d{2}-\d{2}\s+\d{2}:\d{2})
```

Result: `2026-05-16 14:30`

Use `\s+` because the gap between date and time may contain more than one space.

## Example 7: a value in parentheses

Source:

```text
[Urgent] Order confirmation requested (ORD-20260516-0042)
```

Pattern:

```text
\((ORD-\d{8}-\d+)\)
```

Result: `ORD-20260516-0042`

Use `\(` and `\)` to match literal parentheses.

## Example 8: select one value from several numbers

Source:

```text
Product: Keyboard / Quantity: 2 / Unit price: 35000 won / Total: 70000 won
```

To extract only the quantity, include its surrounding label:

```text
Quantity:\s*(\d+)\s*/
```

Result: `2`

Using only `(\d+)` finds the first number in the string. Including the intended value's fixed label is safer.

## Example 9: inconsistent spacing

Source:

```text
Ticket   :    CS-7788
```

Pattern:

```text
Ticket\s*:\s*([A-Z]+-\d+)
```

Result: `CS-7788`

Use `\s*` around separators when copied text has variable spacing.

## Example 10: multiline text

Source:

```text
Order: A-1024
Payment: 35000 won
Status: Complete
```

Pattern:

```text
Payment:\s*([\d,]+) won
```

Result: `35000`

The same approach works on multiple lines when the desired line has a fixed label.

## Choose a pattern quickly

| Situation | Pattern shape | Reason |
| --- | --- | --- |
| Fixed text before and after | `Prefix\s*(.+?)\s*Suffix` | Capture a narrow section |
| Digits only | `(\d+)` | Extract digits without commas |
| Commas in an amount | `([\d,]+)` | Preserve a value such as `48,500` |
| Known code shape | `([A-Z]+-\d+)` | Match letters followed by a number |
| Inconsistent spacing | `\s*` or `\s+` | Tolerate whitespace differences |
| Literal special characters | `\[` `\.` `\(` | Match characters rather than regex syntax |

## Storage rules

- If capture groups exist, save the first group's value.
- Without capture groups, save the whole match.
- An empty pattern saves the entire source string.
- No match saves an empty string.
- An invalid regular expression also saves an empty string without stopping the macro.

## Test a pattern

The extraction editor includes a test area:

1. Paste a real example into Source text.
2. Enter the pattern.
3. Click Extract.
4. Check whether the result is correct.

> [!TIP]
> A small typo can change the result. Test the pattern before saving.

## Troubleshooting

- Check that source and destination names are different when you need to preserve the source.
- Use the variable monitor to verify the actual source string.
- Put the desired part in `()`.
- Use `\s*` where spaces may occur.
- Escape literal dots, brackets, and parentheses with `\`.
- Broad patterns such as `(.+)` can capture too much; include fixed surrounding text when possible.

## Recommended authoring sequence

1. Write the fixed prefix from the source.
2. Put the part to extract in parentheses.
3. Write the fixed suffix.
4. Test the result.

```text
Order:\s*(.+?)\s*/
```

This extracts the value after `Order:` and before `/`.

## Related guides

- [Variables and calculations](07-variables-and-calculations.md)
- [Conditions](04-conditions.md)
- [App introduction and installation](../../README.en.md)
- [Full manual contents](00-contents.md)

## Continue reading

[Manual home](README.md) | [Contents](00-contents.md) | [Previous: 10](10-favorites.md) | [Next: 12](12-sample-steps.md)
