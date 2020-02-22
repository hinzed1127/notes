# Mental Models

Gives simple example with variable assignment

```javascript
let a = 10;
let b = a;
a = 0;
```

Asks "what are the values of a and b after it runs?".

Goes over what the mental models behind calculating that in your head look like:

- using "assign" or "set" when thinking about variables
- e.g. "set `b` to `a`" ... what does that even mean? where have we come up with the language for that description?

Over time, we accumalate a number of different mental models for how we can think about programming. Probably a combination of shorcuts that are:

- Visual
- Spatial
- Mechanical

Sometimes these mental models are incomplete, or simply wrong. The goal here is to rebuild and correct those bad assumptions.

# Coding, Fast and Slow

Mentions Kahneman's "Thinking, Fast and Slow" in the context of coding. Programming over time leads us to use our "fast" pattern-matching system, when sometimes it should be our slow system instead.

Example:

```javascript
function duplicateSpreadsheet(original) {
  if (original.hasPendingChanges) {
    throw new Error("You need to save the file before you can duplicate it.");
  }

  let copy = {
    created: Date.now(),
    author: original.author,
    cells: original.cells,
    metadata: original.metadata
  };
  copy.metadata.title = `Copy of ${original.metadata.title}`;
  return copy;
}
```

While this is pretty quick to grok, it's easy to miss the bug that the copy is altering the original's title and not just its own (in technical terms, javascript objects are passed by reference, and so this mutates the original object, but Dan responded to my email with the hope that he'll explain this in a more intuitive way). This is a situation where our "fast" thinking leads us to overlook a subtle bug.
