# Overview

_Trace Primitives_ (TP) is an extension to the tracer that allows the developer to step through the execution of individual primitives of expressions, examining intermediate results and left and right arguments of sub-expressions. This has been demoed by John Daintree over several user meetings, including:

* [Dyalog 22](https://dyalog.tv/Dyalog22/?v=b2at0Sa8v3E)
* [Dyalog 23](https://dyalog.tv/Dyalog23/?v=CohsPaCIh4s)

TP is now in the version 20 nightly builds, and the purpose of this document is to provide a "getting started" guide to how you use it. It's a powerful addition to the developer's toolbox: it allows for the introspection of complex expressions typed directly into the session, and can be used in conjunction with the traditional tracing mode to skip over lines you're not interested in, and dive into primitives level for the interesting bits. 

**Note**: this document refers to the Windows version of Dyalog APL only.

## Getting started

There are three primary means of starting a TP session. Firstly, there is a new key-combo added (Trace Primitive - TP), currently bound to <kbd>shift</kbd>+<kbd>alt</kbd>+<kbd>enter</kbd> (analogous to the <kbd>control</kbd>+<kbd>enter</kbd> used to start a "normal" trace). This key-combo can be used directly in the session. In the session, enter

```apl
(+/÷≢)⍳10
```
and hit <kbd>shift</kbd>+<kbd>alt</kbd>+<kbd>enter</kbd>. You should see:

![Trace expression](./img/start-tbt.png)

The little red box surrounding the `⍳` is showing the next primitive to be executed. Keep hitting <kbd>shift</kbd>+<kbd>alt</kbd>+<kbd>enter</kbd> a few times to see how the execution progresses through the tacit expression. 

You can also trace primitives by selecting _Trace Primitives..._ from the _Action_ menu:

![Trace expression via Actions menu](./img/trace-primitives-menu-1080.png)

or by selecting _Action > Trace Primitives..._ from the context menu:

![Trace expression via Actions context menu](./img/trace-primitives-context-menu-1080.png)

The other way of instigating a TP session is to use the new _Next Primitive_ symbol in the tracer's toolbar, showing as a downward arrow over three dots:

![Next primitive](./img/next-primitive.png)

Let's write a dfn to try this out:

```apl
Arrow ← { ⍝ Draw an arrow head of size ⍵, direction given by ⍺
    ⍺←0
    ⌽⍤⍉⍣⍺∧∘⌽⍨∘.≤⍨⍳⍵
} 
```

```
      1 Arrow 5
┌→────────┐
↓0 0 0 0 1│
│0 0 0 1 1│
│0 0 1 1 1│
│0 0 0 1 1│
│0 0 0 0 1│
└~────────┘
```

Trace into the expression `1 Arrow 5` with <kbd>control</kbd>+<kbd>enter</kbd>. Execute the first line by hitting <kbd>enter</kbd> (or clicking the Execute Line symbol in the toolbar) like you normally would. On the next line, you can now use the _Next Primitive_ icon to trace through token by token (or use <kbd>
shift</kbd>+<kbd>alt</kbd>+<kbd>enter</kbd>). 

![Trace dfn](./img/trace-dfn-1080.png)

In other words, the _Next Primitive_ icon is always present in the tracer. The new key-combo lets you open a tracer on an expression typed directly in the session that previously could not be traced into. 

## Advanced Primitive Tracing

So far, we've been able to follow the execution _flow_, which is particularly useful when dealing with tacit expressions. The _Trace Primitive_ system can help us further by also showing intermediate left and right arguments and earlier results. These aspects of the tracer UI are disabled by default, but can be picked up from the _Tools > Primitives_ menu. 

![Tools menu](./img/tools-menu.png)

Note that there are close to a dozen entries here -- we won't be covering them all, and in all likelihood, you will probably not need several of them very often.

The key ones are _Left_ and _Right_, representing the left, and right argument about to be passed to the function currently highlighted by the red box. Enable the _Left_ and _Right_ UI elements by selecting them from the menu, and place them as you see fit. Even if you're not a fan of docked windows, it works well visually of having the argument windows docked in the tracer. Step through a few primitives, and observe how the intermediate left, and right arguments change as the execution progresses. 

![Docked left and right args](./img/docked-left-right.png)

The next UI element you may want to consider is _Function_, showing the current function. At first blush, this may seem redundant, as it's already visible by the red box. However, it can be set to render as a tree (like what `]box on -t=tree` does), which occasionally can prove useful when dealing with complex tacit expressions.

![Current function as tree](./img/current-function-as-tree.png)

There are several other UI elements available to you, including those that give you a view of the _previous_ function's arguments and results. Explore those as and when you feel that this is something you need. There is also a UI element showing the current bracket axis.


