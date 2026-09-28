# 6. Pointers: reuse groups of steps

[한국어](../6.%20%ED%8F%AC%EC%9D%B8%ED%84%B0.md) | **English**

[Manual home](README.md) | [Contents](00-contents.md) | [Previous: 5](05-loops.md) | [Next: 7](07-variables-and-calculations.md)

Screenshots show the Korean interface; captions and instructions are in English.

## Pointers

## What is a pointer?

A pointer defines a reusable group of steps that you can call from different places. Use it for common popup handling, saving, or validation procedures.

## Basic structure

A pointer has a definition and a call step:

```text
POINTER START
  Reusable steps
POINTER END

CALL POINTER
```

A call runs the defined steps and then returns to the step after the call.

![Pointer definition and call steps](../img/6.-포인터-01.png)

## Example 1: close a common popup

1. Add Pointer start.
2. Add a condition for the popup image.
3. Put its close-button click inside the condition.
4. Add Pointer end.
5. Insert calls wherever the popup might appear in a longer macro.

If the popup handling changes, edit only the pointer definition.

## Example 2: reuse save-and-wait actions

1. Add Pointer start.
2. Add keyboard action `ctrl+s`.
3. Add a delay.
4. Add Pointer end.
5. Add calls wherever saving is needed.

## Example 3: call a shared task inside a loop

Pointers also work inside loops. For example, run the same validation for each row:

```text
LOOP
  Click row
  CALL POINTER: Common validation
END LOOP
```

![Pointer call inside a loop](../img/6.-포인터-02.png)

## Conditional BREAK inside pointers

A conditional BREAK inside a pointer definition is absorbed at the pointer boundary.

> [!NOTE]
> BREAK ends the pointer and **continues with the step after its call**. It does not affect the caller's condition or loop blocks.

```text
POINTER START: Close popup
  IF error image is found
    Handle error
    BREAK
  END IF
  Click close button
POINTER END

LOOP 10 times
  CALL POINTER: Close popup
  Next task: continues even after BREAK inside the pointer
END LOOP
```

In this example, BREAK skips the remaining pointer steps, including the close-button click, then resumes at Next task. The surrounding loop is not stopped.

**To affect condition or loop handling at the call site, place BREAK outside the pointer, directly inside the relevant conditional flow.**

## Authoring tips

- Use pointers for short, frequently repeated sequences.
- Defining an entire long workflow as one pointer can make the right editing location hard to find.
- Give pointers descriptive names or comments.
- Combine pointers and conditions to isolate popup and exception handling.

## Pre-run pointer checks and call depth

Before playback, the app checks for duplicate pointer IDs and cycles in which pointers repeatedly call one another. Excessive call depth also reaches a runtime safety limit and stops execution.

Keep reusable tasks small and reduce unnecessary nesting. When an error is reported, inspect the indicated definition or call, change duplicate IDs, break call cycles, or reduce call depth before trying again.

## Related guides

- [Loops](05-loops.md): call pointers during repetitions.
- [Conditions](04-conditions.md): group popup and exception handling.
- [App introduction and installation](../../README.en.md)
- [Full manual contents](00-contents.md)

## Continue reading

[Manual home](README.md) | [Contents](00-contents.md) | [Previous: 5](05-loops.md) | [Next: 7](07-variables-and-calculations.md)
