# Document Editor - Low Level Design (LLD)

## Overview

This repository contains the **Low Level Design (LLD)** for a simple **Document Editor Application**.
The purpose of this project is to demonstrate object-oriented design principles and common design patterns used in document editing systems.

The system supports:

- Adding text elements
- Adding image elements
- Rendering the document
- Saving the document using different persistence mechanisms

This design is intended as a **learning project for system design and OOP concepts**.

---

# Architecture Overview

The document editor is composed of four main components:

1. **Document Editor**
2. **Document Model**
3. **Document Elements**
4. **Persistence Layer**

```
DocumentEditor
     |
     v
  Document
     |
     v
DocumentElement (Abstract)
     |
     ├── TextElement
     └── ImageElement

Persistence (Abstract)
     |
     ├── SaveToFile
     └── SaveToDB
```

---

# Class Design

## 1. DocumentElement (Abstract Class)

This is the base class for all elements that can exist inside a document.

### Responsibilities

- Defines a common interface for document elements.
- Ensures all elements implement the `render()` method.

### Methods

```
render()
```

### Implementations

- `TextElement`
- `ImageElement`

---

## 2. TextElement

Represents a text block inside the document.

### Methods

```
render()
```

### Example Responsibility

Rendering textual content when the document is displayed.

---

## 3. ImageElement

Represents an image inside the document.

### Methods

```
render()
```

### Example Responsibility

Rendering an image from a provided image path.

---

## 4. Document

Represents the complete document being edited.

### Attributes

```
doc_elements : List<DocumentElement>
```

### Methods

```
addElement(DocumentElement element)
render()
```

### Responsibilities

- Maintains a list of document elements.
- Handles rendering of the entire document by iterating through elements.

---

## 5. Persistence (Abstract Class)

Defines the interface for saving documents.

### Methods

```
save(Document document)
```

### Implementations

#### SaveToFile

Saves the document to a file system.

#### SaveToDB

Saves the document to a database.

This abstraction allows the system to change storage mechanisms without modifying the editor logic.

---

## 6. DocumentEditor

This is the main class that coordinates operations.

### Attributes

```
Document doc
Persistence db
```

### Methods

```
addText(string text)
addImage(string imagePath)
renderDoc()
save()
```

### Responsibilities

- Adds content to the document
- Triggers rendering
- Saves the document using the configured persistence method

---

# Design Principles Used

## 1. Abstraction

`DocumentElement` and `Persistence` provide abstract interfaces that allow multiple implementations.

---

## 2. Open/Closed Principle

New document elements can be added without modifying existing classes.

Example:

```
VideoElement
TableElement
ChartElement
```

---

## 3. Separation of Concerns

The design separates:

- Document structure
- Rendering logic
- Persistence logic

---

# SOLID PRINCIPLES FOLLOWED

- [x] Single Responsibility Principle (SRP)
- [x] Open Close Principle (OCP)
- [x] Liskov Substitution Principle (LSP)
- [x] Interface Segregation Principle (ISP)
- [x] Dependency Inversion Principle (DIP)

# Design Patterns Used

## Composite Pattern

The `Document` contains multiple `DocumentElement` objects.

```
Document
 ├ TextElement
 ├ ImageElement
 └ TextElement
```

This allows treating individual elements and collections uniformly.

---

## Strategy Pattern

The persistence mechanism can be swapped dynamically.

Example:

```
Persistence p = new SaveToFile()
Persistence p = new SaveToDB()
```

---

# UML Diagram

The following diagram illustrates the system design.

![Document Editor UML](./LLD/DocumentEditor/Document Editor LLD.png)

---

# Example Workflow

1. Create a `DocumentEditor`
2. Add text or images
3. Render the document
4. Save the document

Example flow:

```
editor.addText("Hello World")
editor.addImage("image.png")

editor.renderDoc()

editor.save()
```

---

# Possible Future Improvements

This design can be extended with additional features:

- Undo / Redo functionality
- Rich text formatting
- Table support
- Video or embedded media
- Collaborative editing
- Version control
- Cursor and selection management

---

# Purpose of This Project

This project is meant to practice:

- Object Oriented Design
- Low Level System Design
- UML Modeling
- Design Patterns

It is not a full production editor but a **learning exercise for software architecture.**

---

# Author

Designed as a learning project for **Low Level System Design practice.**
