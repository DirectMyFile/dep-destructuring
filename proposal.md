# Destructuring

## Contact information

**Name**: Kenneth A. Endfinger

**Email**: kaendfinger@gmail.com

**GitHub Username**: kaendfinger

[Proposal Location](https://github.com/DirectMyFile/dep-destructuring)

## Summary

Allow values to be destructured on assignment.

## Motivation

Problems to solve:

- Assigning variables from large maps and lists can often be cumbersome and look rather ugly.
  One way to solve this is to allow developers to assign multiple variables in one go, in a simple and easy to understand manner.

## Examples

### Property Destructuring

```dart
class Point {
  final int x;
  final int y;

  Point(this.x, this.y);
}

var {x, y} = new Point(5, 1);

assert(x == 5);
assert(y == 1);
```

### List Destructuring

```dart
var [x, y] = [5, 2];

assert(x == 5);
assert(y == 2);
```

### Value Swapping

```dart
var [a, b] = [1, 2];
[a, b] = [b, a];

assert(a == 2);
assert(b == 1);
```

### With Typing

```dart
var [String a, int b] = ["Hello World", 5];

assert(a == "Hello World");
assert(b == 5);
```

### Usage with Access

```dart
target.[a, b] = [1, 2];
```

## Proposal

Destructuring should be allowed in any kind of assignment. Identifiers should be separated by a `,` with optional whitespace.

### Semantics

The following is what should happen when evaluating a destructuring assignment.

The value on the right should be evaluated, and the values should be assigned to the respective variables left to right.

The result of the expression should always be the right hand side of the expression.

#### Property Destructuring

It is a static warning if an variable identifier does not correspond to a property of the right hand side, unless the right hand side is marked as a proxy.

#### List Destructuring

It is a runtime error if the number of identifiers on the left hand side is out of range of the right hand side list.

### Current Syntax Equivalent

The behavior of the destructuring should be equivalent to the given code that does not use this proposal's syntax.

```dart
/// With this Proposal
var [a, b] = [1, 2];

/// Without this Proposal
var tmp = [1, 2];
var a = tmp[0];
var b = tmp[1];
```

```dart
/// With this Proposal
var [String a, int b] = ["Hello", 5];

/// Without this Proposal
var tmp = ["Hello", 5];

String a = tmp[0];
int b = tmp[1];
```

```dart
class Point {
  final int x;
  final int y;

  Point(this.x, this.y);
}

/// With this Proposal
var {x, y} = new Point(5, 1);

/// Without this Proposal
var tmp = new Point(5, 1);
var x = tmp.x;
var y = tmp.y;
```

```dart
class Point {
  final int x;
  final int y;

  Point(this.x, this.y);
}

/// With this Proposal
var {int x, int y} = new Point(5, 1);

/// Without this Proposal
var tmp = new Point(5, 1);
int x = tmp.x;
int y = tmp.y;
```

## Alternatives

### Syntax

Alternative Syntax A:
```dart
var [x, y] = [1, 2];
```

Alternative Syntax B:
```dart
var x, y = [1, 2];
```

## Implications and limitations

- This must also work in for-in loops:

```dart
for(var {a, b} in pairs) {
  print("$a:$b");
}
```

## Deliverables

### Language specification changes

The changes described above should be incorporated into the specification.

### A working implementation

No working implementation is available, although one can experience this syntax in practice by using languages that have this feature already.

### Tests

**TODO**

## Patents rights

TC52, the Ecma technical committee working on evolving the open [Dart standard][], operates under a royalty-free patent policy, [RFPP][] (PDF). This means if the proposal graduates to being sent to TC52, you will have to sign the Ecma TC52 [external contributor form][] and submit it to Ecma.

[tex]: http://www.latex-project.org/
[language spec]: https://www.dartlang.org/docs/spec/
[dart standard]: http://www.ecma-international.org/publications/standards/Ecma-408.htm
[rfpp]: http://www.ecma-international.org/memento/TC52%20policy/Ecma%20Experimental%20TC52%20Royalty-Free%20Patent%20Policy.pdf
[external contributor form]: http://www.ecma-international.org/memento/TC52%20policy/Contribution%20form%20to%20TC52%20Royalty%20Free%20Task%20Group%20as%20a%20non-member.pdf
