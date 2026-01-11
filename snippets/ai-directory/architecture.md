# Architecture Documentation Reference

This is a guide for what to include when documenting architecture, not a template to copy.

## When to Create

Create `architecture.md` when:
- The system has multiple components that interact
- Data flows through the system in non-obvious ways
- There are important design decisions worth capturing
- A new contributor would need context to understand the structure

Don't create it:
- At project init (nothing to document yet)
- For simple scripts or single-file projects
- Just to have a file

## What to Cover

### Overview
What does this system do? One paragraph.

### Components
Major pieces and their responsibilities. How do they relate?

### Data Flow
How does data move through the system? Consider:
- Entry points (user input, API calls, events)
- Transformations (what happens to data)
- Exit points (output, storage, external calls)

### Key Decisions
Important architectural choices and why they were made. This is often the most valuable section - it captures context that would otherwise be lost.

### Dependencies
External systems, libraries, or services this depends on.

### Extension Points
Where and how to add new functionality.

## Keep It Current

Architecture docs rot quickly. Update when:
- Adding new components
- Changing how components interact
- Making significant design decisions
- Discovering the doc is wrong
