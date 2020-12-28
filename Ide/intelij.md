# Shortcuts

CTRL + y  - remove whole line

## F2

We don’t want to use the mouse when navigating between errors and warnings in the editor, so use [F2 to jump to the next error, warning or suggestion](https://www.jetbrains.com/help/idea/navigating-through-the-source-code.html#navigate-errors-warnings). Combine this with either Alt+Enter, to see all suggestions and pick one, or Shift+Alt+Enter to apply the first suggestion.

## Ctrl+E

This pops up the recent files box which you can navigate using arrow keys. We can also open tool windows from here, including ones that don’t have keyboard shortcuts. Like any window in IntelliJ IDEA we can search for something specific in here by typing.

## Ctrl+B

We often want to navigate the code from within the code. With ⌘B (MacOS), or Ctrl+B (Windows/Linux) we can [go to the declaration](https://www.jetbrains.com/help/idea/navigating-through-the-source-code.html#go_to_declaration) of a symbol. For example, pressing this on a field will take the cursor to the field declaration. Pressing it on a class name will take us to the class file. 

## Ctrl + W / Shift + Ctrl + W

We can select increasing or decreasing sections of code near the cursor with ⌥ and Up or Down arrows (MacOS) and Ctrl+W or Ctrl+Shift+W (Windows/Linux). When [extending the selection](https://www.jetbrains.com/help/idea/working-with-source-code.html#editor_code_selection), IntelliJ IDEA automatically selects the next valid expression in increasing sections. ⌥↓ (MacOS) or Ctrl+Shift+W (Windows/Linux), will decrease the selection again all the way back to the cursor.

## Shift+Ctrl+Enter

[Complete Current Statement,](https://www.jetbrains.com/help/idea/working-with-source-code.html#142f8b57) if we’re in the habit of using complete current statement while you’re coding, most of the time it will simply add a semi-colon to the end of the code. But it works for more complex code, for example if you press it while you’re writing a “for” loop, IntelliJ IDEA will add the curly braces and place your cursor inside the block. In an “if” statement, it can add the parentheses and curly braces and again place your cursor in the correct spot. 

## Shift+Ctrl+Alt+T

When we press this shortcut on a symbol or selection we are [shown the refactoring options available](https://www.jetbrains.com/help/idea/refactoring-source-code.html#refactoring_invoke). We can select one with the arrow keys and enter, or we can use the number to the left of the refactoring to select it. 

# Debuging

![img](https://springframework.guru/wp-content/uploads/2020/04/Debugger-panel.jpg)

On the left side, we have a list of frames. Frames let us navigate the call stack, so we can easily see how we got to the point where we put the breakpoint we are currently at. You can also switch threads call stacks, using little drop down above.

On the right side, we have a list of watches. Watches are a list of variables or computed expressions that have values corresponding to the current place debugger is at. You can think of them as a snapshot of data in the application. More on that later.

![img](https://springframework.guru/wp-content/uploads/2020/04/Debugger-stepping.jpg)

We have several icons here, describing from the left:

- **Step over (F8)** – goes over the line, skipping internals of the code it skipped (for example, stepping over the method call, will not move debugger into that method)
- **Step into (F7)** – moves debugger into the internals of code currently on debug point (for example, if we are stopped on a method call, it will move into that method body)
- **Force step into (Alt +Shift + F7)** – useful if sometimes method call is skipped with normal Step into, forcing it inside
- **Step out (Shift + F8)** – it goes out of the current method into the caller code
- **Drop frame** – allows us to drop the last stack call, and go back to the previous one
- **Run to cursor (Alt + F9)** – continues execution until the caret position is reached

## Advanced breakpoint

For example, let us assume, that something wrong happens only for a ninth element in the list. It will be hard to make a fix and skip debugging all the way until we reach the desired point in the ninth loop round, just to see that it was a bad fix. There is a way to solve that.

If we put a breakpoint inside the loop and click that small red dot near line number using a right mouse button, we will open advanced breakpoint options:

![img](https://springframework.guru/wp-content/uploads/2020/04/Advanced-breakpoint.jpg)

Here we have a “condition” field, where we can insert, for example, i == 9. Thanks to that, when we run the debugger, it will stop on this breakpoint only if i equals 9!

We may also disable stopping on a breakpoint if we do not want to remove it, but also do not want a debugger to stop on it.

If we uncheck the “Suspend” checkbox, then we will have even more options to choose from.

[![img](https://springframework.guru/wp-content/uploads/2020/04/Advanced-breakpoint-2.jpg)](https://springframework.guru/wp-content/uploads/2020/04/Advanced-breakpoint-2.jpg)

We have the option to log the message that breakpoint was hit (Log “breakpoint hit” message) or full stack trace (Log stack trace). There is an option to evaluate an expression and log this instead (Evaluate and log). A breakpoint may be removed, once it’s hit (Remove once hit). There are also several filters and a pass count.

### Changing variable value

During the debugging session, it is possible to alter the values of variables and object properties. It may be useful if we want to test methods using values that may be hard to generate with the most usual run path.

In the second example above, we have used a loop that we will use to show how to change variable value.

If we set a breakpoint on the line with the modulo condition, we will have i variable in watches. If we click on that watch with right-click and select set value we will be able to alter the value of that variable:

[![img](https://springframework.guru/wp-content/uploads/2020/04/watch-value-change.jpg)](https://springframework.guru/wp-content/uploads/2020/04/watch-value-change.jpg)

Try to change that to 6 and as a result of the program we will have such output:

[![img](https://springframework.guru/wp-content/uploads/2020/04/Watch-change-result.jpg)](https://springframework.guru/wp-content/uploads/2020/04/Watch-change-result.jpg)