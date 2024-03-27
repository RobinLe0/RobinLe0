# C/C++ Code Guidelines
The guidelines in these guidelines are to be applied to all new code added to the RobinLe repos.

> [!NOTE]
> I'm still in the process of making all my repositories comply with these guidelines.





## General

### Languages
All code and documentation is written in English, and applications also use English as their primary
language.

Translation may be offered for documentation and applications.



### Target Platform
Creating portable code is not the main goal - however, wherever possible, platform-dependent code
should be avoided.

The main target platform is 64-bit Windows. 32-bit compatibility might be provided in special cases.



### DLL Interface
All my DLLs are C-compatible with `__stdcall` as a calling convention.

`.lib` files provided are for Visual Studio 2015+ (as those are all binary-compatible when working with the most recent version of Visual Studio).



### `.gitignore`
If a repository produces binary output, this output cannot be commited.



### Links to other repos/files
No direct links to any git hosting service are supplied.

Instead, the URL shortener `rle.sh` is used with the following scheme:

| Base URL (always the same) | Repository name |
|----------------------------|-----------------|
| `https://rle.sh/git/`      | `RobinLe1402`   |

The only exception is functionality that is service-specific, like GitHub's
[star list](https://github.com/RobinLe1402?tab=stars) which lets you add repos to lists, and thereby
categorize them.

#### Examples
* `https://rle.sh/git/RobinLe1402/#readme`
* `https://rle.sh/git/RobinLe1402/tags`
* `https://rle.sh/git/RobinLe1402/releases`





## Source Code

### Filenames

#### File Extensions

| Category | C\*  | C++    |
|----------|------|--------|
| Header   | `.h` | `.hpp` |
| Source   | `.c` | `.cpp` |

(\* either a pure C file or a file compatible with C, e.g. via `#ifdef __cplusplus`)



### Text Encoding
All source files are to be saved as ASCII files. Non-ASCII characters have to be escaped,
e.g. like so: `u8"Großosteim"` &rarr; `u8"Gro\u00DFostheim"`.

An exception to this rule are markdown files like this one.



### Maximum Line Length
By default, a line of code shouldn't be wider than 100 characters.

In special cases, however, this can be ignored.



### Documentation
Source code documentation is done via XML documentation comments:
```cpp
/// <summary>What does the function do?</summary>
/// <param name="b">What does this parameter mean?</param>
/// <returns>What does the return value mean?</returns>
int DoSomething(bool b);
```



### Naming Conventions
> [!INFO]
> In C (which I usually use for dynamic libraries), a prefix like `rlText_` might be added to group
> the identifiers of that library.

| Category | Convention | Example |
|----------|------------|---------|
| Types    | PascalCase | `class TestClass` |
| Method   | camelCase  | `void TestClass::doSomething();` |
| Method (static) | PascalCase | `void TestClass::DoSomething();` |
| Variables | Hungarian Notation + PascalCase | `int iTest;` |
| Member Variables (non-public) | `m_` as prefix | `int m_iTest;` |
| Member Variables (static, non-public) | `s_` as prefix | `static int s_iTest;` |
| Defines  | UPPERCASE  | `#define RL_TEST 14` |
| Constants | Hungarian Notation + PascalCase | `constexpr int iTest = 2;` |



### Referenced files
Files referenced in my repositories cannot be located outside that repository.

Exceptions to this rule are...
* binaries (`*.exe`/`*.dll`)
* big binary resources (like video files/large image files/...)
* headers of another library

If any of these exceptions is applied, it has to be documented in the corresponding `README.md`
file.



### Formatting
My source files use **tabs**, not **spaces** for indenting source code.

However, spaces may be used to get parts of source code to align to other code
(in a monospace font), like so:
```cpp
int test()
{
[tab]if (bConditionA && (bConditionB || bConditionC)
[tab][    spaces    ]&& (bConditionD || bConditionD))
[tab][tab]return 1;
[tab]else
[tab][tab]return -1;
}
```



#### Curly brackets
The opening and the closing curly bracket of a code block are always the first thing in a line
(apart from whitespace).

An exception to this rule is the two are on the same line, as in
`while (i < 5) {++i}` or `while (b) {}`

Moreover, an `else` is never on the same line as the closing curly bracket of the previous `if`.



### Constructors/Destructors/Assignment Operators
Custom constructors, destructors and assignment operators (`operator=`) are to be avoided wherever
possible.

However, in some cases, using these can make the use of a class **way** easier. In these cases,
`= default` should be used wherever possible.



### Functionality not to be used
* Bitfields
* `new` and `delete` (&rarr; smart pointers), except in special cases



### Unpopular functionality that may be used
* `goto` (if it makes the code **significantly** less complicated)





## Runtime Behaviour

### Internal Text Encoding
All strings must be either UTF-8 encoded or pure ASCII.

In C++ source code, the type to be used is `std::u8string` or, for backwards
compatibility with older versions of C++, `std::string`.

In C files, the type to be used is `char8_t *` or, for backwards compatibility with older versions
of C, `char *`

An exception to this rule is interfacing with APIs that require a different encoding, like the
Win32 API which requires UTF-16 `wchar_t *`.

> Repositories that comply with this rule display the following badge in their README:
> 
> <img src="/res/badges/utf8.svg" width="50px"/>
