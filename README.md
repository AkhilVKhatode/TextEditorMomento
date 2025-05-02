# Memento Pattern in Python

This repository contains a Python implementation of the **Memento Pattern**. The Memento Pattern is a behavioral design pattern that allows you to capture and restore an object's state without violating its encapsulation. It is useful for implementing features like "undo" functionality in applications.

## Overview

The program demonstrates a basic text editor that allows the user to:
1. Type text.
2. Save the text state.
3. Undo text changes to restore previous states.

### Key Components

- **TextEditor**: The class representing a simple text editor where you can set and get the text.
- **Memento**: Represents a snapshot of the current state (text) in the `TextEditor` class.
- **EditorHistory**: Manages a stack of mementos (text snapshots) to enable undo functionality.

## Classes

### `TextEditor`
The `TextEditor` class allows the user to set and get text. It also provides methods to save and restore the text state.

- **Methods**:
  - `set_text(text: str)`: Sets the current text.
  - `get_text()`: Returns the current text.
  - `save()`: Saves the current text state as a memento.
  - `restore(memento: Memento)`: Restores the text state from a given memento.

### `Memento`
The `Memento` class holds the state (text) of the `TextEditor` at a specific point in time.

- **Methods**:
  - `get_text()`: Returns the saved text state.

### `EditorHistory`
The `EditorHistory` class maintains a stack of mementos and allows pushing and popping of mementos to manage the history of text states.

- **Methods**:
  - `push(memento: Memento)`: Adds a memento to the history stack.
  - `pop()`: Removes and returns the last memento from the history stack.

## Output Example
```text
Copy
Current text: Hello
Current text: Hello, World!
Current text: Hello, World! Welcome to Memento Pattern.
After undo, text: Hello, World!
After second undo, text: Hello
```



### Update - Redo feature implemented
```python
class TextEditor:
    def __init__(self):
        self.text = ""

    def set_text(self, text):
        self.text = text

    def get_text(self):
        return self.text

    # Creates a memento (snapshot) of the current state
    def save(self):
        return Memento(self.text)

    # Restores the state from the given memento
    def restore(self, memento):
        self.text = memento.get_text()


class Memento:
    def __init__(self, text):
        self.text = text

    def get_text(self):
        return self.text


class EditorHistory:
    def __init__(self):
        self.undo_stack = []
        self.redo_stack = []

    # Save new state; clear redo stack when a new state is saved
    def save_state(self, memento):
        self.undo_stack.append(memento)
        self.redo_stack.clear()

    # Undo operation: push current state to redo stack and return last state from undo stack
    def undo(self, current_state):
        if self.undo_stack:
            self.redo_stack.append(current_state)
            return self.undo_stack.pop()
        return None

    # Redo operation: push current state to undo stack and return last state from redo stack
    def redo(self, current_state):
        if self.redo_stack:
            self.undo_stack.append(current_state)
            return self.redo_stack.pop()
        return None


# Memento Pattern with Undo/Redo Demo
if __name__ == "__main__":
    editor = TextEditor()
    history = EditorHistory()

    # Initial state
    editor.set_text("Hello")
    history.save_state(editor.save())
    print("Current text:", editor.get_text())

    # First change
    editor.set_text("Hello, World!")
    history.save_state(editor.save())
    print("Current text:", editor.get_text())

    # Second change
    editor.set_text("Hello, World! Welcome!")
    print("Current text:", editor.get_text())

    # Undo the last change
    previous_state = history.undo(editor.save())
    if previous_state:
        editor.restore(previous_state)
        print("After undo, text:", editor.get_text())

    # Redo the undone change
    redo_state = history.redo(editor.save())
    if redo_state:
        editor.restore(redo_state)
        print("After redo, text:", editor.get_text())
```
