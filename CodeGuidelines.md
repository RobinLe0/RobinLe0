# C/C++ Code Guidelines
The guidelines in these guidelines are to be applied to all new code added to the RobinLe repos.
However, they're not guaranteed to be applied everywhere at this time.


## Text Encoding
### Source Files
All source files are to be saved as ASCII files. Non-ASCII characters have to be escaped,
e.g. like so: `u8"Groﬂosteim"` &rarr; `u8"Gro\x00DFostheim"`.

An exception to this rule are markdown files like this one.

### Applications at Runtime
All strings must be either UTF-8 encoded or pure ASCII.

In C++ source code, the type to be used is `std::u8string` or, for backwards
compatibility with older versions of C++, `std::string`.

In C files, the type to be used is `char8_t *` or, for backwards compatibility with older versions
of C, `char *`

An exception to this rule is interfacing with APIs that require a different encoding, like the
Win32 API which requires UTF-16 `wchar_t *`.

| :warning: This rule has not yet been applied everywhere at this point. |
|--|
| The following repositories comply with this rule:     |
| [`rlText_Dynamic`](https://rle.sh/git/rlText_Dynamic) |


## Source Code Formatting

### Curly brackets
With `if` `else if`, `else`, `while`, `do`, `for` or class/struct/union declarations, the opening curly bracket, `{`,
is always on the next line.

An exception to this rule is if the closing curly bracket is on the same line, as in
`while (i < 5) {++i}` or `while (b) {}`

Moreover, an `else` is never on the same line as the closing curly bracket of the previous `if`.


## Functionality not to be used
* Bitfields

## Unpopular functionality that may be used
* `goto` (if it makes the code **significantly** less complicated)