# Command Pattern

An overview of the **Command Pattern** as presented in *Head First Design Patterns* (Chapter 6, the Remote Control example).

## Definition

The Command Pattern **encapsulates a request as an object**, thereby letting you parameterize other objects with different requests, queue or log requests, and support undoable operations.

**Category:** Behavioral pattern

## Intent

Decouple the object that **requests** an action (the invoker) from the object that **performs** it (the receiver), by placing a command object between them. The invoker only knows that a command can be executed. It does not know what the command does or who carries it out.

## Participants

| Role | Responsibility | Examples in this project |
|---|---|---|
| **Command** | Interface declaring `execute()` and `undo()` | `Command` |
| **ConcreteCommand** | Binds a receiver to an action and implements `execute()` by calling the receiver | `LightOnCommand`, `CeilingFanHighCommand`, `StereoOnWithCDCommand` |
| **Receiver** | Knows how to perform the real work | `Light`, `CeilingFan`, `Stereo` |
| **Invoker** | Holds commands and triggers them, with no knowledge of receivers | `RemoteControl` |
| **Client** | Creates commands, assigns receivers, and loads commands into the invoker | `RemoteLoader` |

## What to Implement

- [ ] **Command interface** with `execute()` and `undo()`
- [ ] **Receivers:** `Light`, `CeilingFan` (with speed states), `Stereo`
- [ ] **Simple commands:** light on/off, stereo on (with CD) / off
- [ ] **Stateful commands for undo:** ceiling fan high / medium / low / off, each remembering the previous speed
- [ ] **NoCommand (Null Object):** default for empty slots, removing null checks
- [ ] **Invoker (`RemoteControl`):** slots for on/off commands, plus a record of the last command for undo
- [ ] **MacroCommand:** executes several commands as one, and undoes them in reverse order
- [ ] **Client class:** wires receivers, commands, and the invoker together
- [ ] *Optional:* request queue and request logging, which cover the "queue or log requests" part of the definition

## Design Principles Involved

| Principle | How it applies |
|---|---|
| **Encapsulate what varies** | The requested action varies, so each action is encapsulated in its own command object |
| **Program to an interface, not an implementation** | The invoker depends only on the `Command` interface |
| **Strive for loosely coupled designs** | Invoker and receiver never reference each other directly |
| **Open-Closed Principle** | New actions are added as new commands without modifying the invoker |
| **Single Responsibility Principle** | The invoker triggers, the command binds, the receiver performs |
| **Favor composition over inheritance** | A command *has a* receiver, and a macro *has* commands, assembled at runtime |

**Related idiom:** Null Object (`NoCommand`).

## Benefits and Trade-offs

**Benefits**
- Complete decoupling of invoker and receiver
- Requests become objects that can be stored, passed, queued, and logged
- Undo, redo, and macros come naturally
- Easy to extend without changing existing code

**Trade-offs**
- Many small classes, typically one per action
- Undo requires commands to store state
- Overkill when a direct method call is enough

## When to Use

- Parameterizing objects with actions (buttons, menu items)
- Queuing, scheduling, or logging requests (job queues, transaction logs)
- Supporting undo and redo
- Grouping operations into macros

## Reference

Freeman, E., Robson, E. *Head First Design Patterns*, Chapter 6: "Encapsulating Invocation: The Command Pattern".
