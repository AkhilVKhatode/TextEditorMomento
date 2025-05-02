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
