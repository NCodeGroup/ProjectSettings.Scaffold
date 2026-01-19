# Copilot Instructions

## Test Project Conventions

### Test File Location and Namespace

Unit test files must mirror the folder structure and namespace of the code under test:

- Test files go in the same relative folder path within the test project
- Test namespace matches the production namespace with `.Tests` suffix

```
// Production code
NCode.Mediator/Wrappers/CommandExceptionHandlerWrapper.cs
namespace NCode.Mediator.Wrappers;

// Test code
NCode.Mediator.Tests/Wrappers/CommandExceptionHandlerWrapperTests.cs
namespace NCode.Mediator.Tests.Wrappers;
```

### Unit Test Style

When writing or modifying unit tests in this project:

- **Do NOT use** `// Arrange`, `// Act`, `// Assert` comments in test methods
- Use blank lines to separate the logical sections of a test instead of comments
- Keep tests concise and readable without AAA comment annotations

### Example

```csharp
[Fact]
public void MyMethod_WhenCondition_ExpectedBehavior()
{
    var input = "test";

    var result = MyMethod(input);

    Assert.Equal("expected", result);
}
```

## Code Style Conventions

### Collection Expressions

Use C# 12+ collection expressions instead of traditional array/collection initialization:

```csharp
// Preferred
byte[] data = [1, 2, 3, 4, 5];
List<string> names = ["Alice", "Bob"];
int[] empty = [];

// Avoid
var data = new byte[] { 1, 2, 3, 4, 5 };
var names = new List<string> { "Alice", "Bob" };
var empty = Array.Empty<int>();
```

### Constants for Literals

Use `const` for any literal values of any type instead of `var`:

```csharp
// Preferred
const string expected = "hello";
const int count = 5;
const char separator = ',';
const double rate = 0.15;

// Avoid
var expected = "hello";
var count = 5;
var separator = ',';
var rate = 0.15;
```

### UTF-8 String Literals

Use C# 11+ UTF-8 string literals (`u8` suffix) when working with byte arrays that represent valid UTF-8 text:

```csharp
// Preferred
var bytes = "Hello"u8.ToArray();
var utf8Bytes = "cafÃ©"u8.ToArray();
var emojiBytes = "ðŸ˜€"u8.ToArray();

// Avoid
byte[] bytes = [72, 101, 108, 108, 111];
byte[] utf8Bytes = [0xC3, 0xA9]; // 'Ã©' in UTF-8
byte[] emojiBytes = [0xF0, 0x9F, 0x98, 0x80]; // ðŸ˜€ in UTF-8
```

Note: Use explicit byte arrays for invalid UTF-8 sequences or when testing error conditions.

## Code Quality

### ReSharper/IDE Warnings

Always fix ReSharper and IDE warnings/suggestions when modifying code. Common fixes include:

- Use collection expressions where applicable (but cast when needed for generic type inference, e.g., `(byte[])[1, 2, 3]` for `ReadOnlyMemory<T>` parameters)
- Remove redundant type specifications
- Use `const` for compile-time constant values
- Ensure all record struct properties are accessed to avoid "never accessed" warnings

### xUnit Assertion Best Practices

Use the appropriate xUnit assertions for collection sizes instead of `Assert.Equal`:

```csharp
// Preferred
Assert.Empty(collection);           // For count == 0
Assert.Single(collection);          // For count == 1

// Avoid
Assert.Equal(0, collection.Count);
Assert.Equal(1, collection.Count);
```

For counts greater than 1, `Assert.Equal(expectedCount, collection.Count)` is acceptable.

### Test Organization with Regions

Organize unit tests within a test class using `#region` directives to group tests by the method or property under test:

```csharp
public class MyClassTests
{
    #region Constructor Tests

    [Fact]
    public void Constructor_WithValidInput_CreatesInstance()
    {
        // test code
    }

    [Fact]
    public void Constructor_WithNullInput_ThrowsException()
    {
        // test code
    }

    #endregion

    #region MyMethod Tests

    [Fact]
    public void MyMethod_WhenCondition_ExpectedBehavior()
    {
        // test code
    }

    #endregion

    #region MyProperty Tests

    [Fact]
    public void MyProperty_ReturnsExpectedValue()
    {
        // test code
    }

    #endregion
}
```

Region naming conventions:
- Use `Constructor Tests` for constructor tests
- Use `{MethodName} Tests` for method tests (e.g., `Dispose Tests`)
- Use `{PropertyName} Property Tests` for property tests (e.g., `Span Property Tests`)
- Use `Generic Type Tests` for tests verifying generic type parameter behavior

### Moq Conventions

All mock setups must use `.Verifiable()` at the end of the setup chain.

Always use `x` as the lambda parameter name in Setup and Verify calls:

```csharp
// Preferred
mockService
    .Setup(x => x.DoSomething(It.IsAny<string>()))
    .Returns("result")
    .Verifiable();

// Avoid
mockService
    .Setup(s => s.DoSomething(It.IsAny<string>()))
    .Returns("result");
```

This ensures that mock setups are explicitly verified and makes tests more maintainable.

### InternalsVisibleTo for Testing

Projects under test should include `InternalsVisibleTo` attributes to enable mocking of internal types and members:

```csharp
// In Properties/AssemblyInfo.cs or a dedicated file
using System.Runtime.CompilerServices;

[assembly: InternalsVisibleTo("DynamicProxyGenAssembly2")]
[assembly: InternalsVisibleTo("ProjectName.Tests")]
```

- `DynamicProxyGenAssembly2` is required for Moq to create proxies for internal types
- The test project name should match the actual test assembly name

This allows unit tests to directly mock internal interfaces and virtual methods, enabling more thorough testing of implementation details.
