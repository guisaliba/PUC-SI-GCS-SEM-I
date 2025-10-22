# Code Conventions

This document outlines the code conventions and standards for this project. Following these conventions ensures consistency, readability, and maintainability across the codebase.

## Table of Contents

- [General Principles](#general-principles)
- [File Organization](#file-organization)
- [Naming Conventions](#naming-conventions)
- [Code Style](#code-style)
- [Comments and Documentation](#comments-and-documentation)
- [Testing](#testing)
- [Error Handling](#error-handling)
- [Security](#security)

## General Principles

### DRY (Don't Repeat Yourself)
- Avoid code duplication
- Extract reusable code into functions, modules, or utilities
- Use inheritance and composition appropriately

### KISS (Keep It Simple, Stupid)
- Write simple, straightforward code
- Avoid over-engineering solutions
- Prefer clarity over cleverness

### YAGNI (You Aren't Gonna Need It)
- Don't add functionality until it's needed
- Focus on current requirements
- Avoid premature optimization

### SOLID Principles
- **S**ingle Responsibility Principle
- **O**pen/Closed Principle
- **L**iskov Substitution Principle
- **I**nterface Segregation Principle
- **D**ependency Inversion Principle

## File Organization

### Project Structure

```
project-root/
├── src/                    # Source code
│   ├── components/         # Reusable components
│   ├── services/           # Business logic services
│   ├── utils/              # Utility functions
│   ├── models/             # Data models
│   └── config/             # Configuration files
├── tests/                  # Test files
│   ├── unit/               # Unit tests
│   ├── integration/        # Integration tests
│   └── e2e/                # End-to-end tests
├── docs/                   # Documentation
├── scripts/                # Build and utility scripts
└── public/                 # Static assets
```

### File Naming

- Use lowercase with hyphens for file names: `user-service.js`
- Test files should mirror source file names with `.test` or `.spec` suffix: `user-service.test.js`
- Use descriptive names that reflect the file's purpose
- Group related files in appropriately named directories

## Naming Conventions

### Variables and Functions

- Use `camelCase` for variables and functions
- Use descriptive names that convey purpose
- Boolean variables should be prefixed with `is`, `has`, `should`, etc.
- Avoid single-letter names except for loop counters

```javascript
// Good
const userName = 'John Doe';
const isUserActive = true;
const hasPermission = checkPermission(user);

function calculateTotalPrice(items) {
  // implementation
}

// Bad
const u = 'John Doe';
const active = true;
const x = checkPermission(user);

function calc(i) {
  // implementation
}
```

### Constants

- Use `UPPER_SNAKE_CASE` for constants
- Define constants at the top of the file or in a dedicated constants file

```javascript
const MAX_RETRY_ATTEMPTS = 3;
const API_BASE_URL = 'https://api.example.com';
const DEFAULT_TIMEOUT = 5000;
```

### Classes

- Use `PascalCase` for class names
- Use nouns for class names
- Keep class names concise but descriptive

```javascript
class UserService {
  // implementation
}

class PaymentProcessor {
  // implementation
}
```

### Interfaces and Types (TypeScript)

- Use `PascalCase` for interfaces and types
- Prefix interfaces with `I` only if it improves clarity (project-specific)

```typescript
interface UserProfile {
  id: string;
  name: string;
  email: string;
}

type HttpMethod = 'GET' | 'POST' | 'PUT' | 'DELETE';
```

## Code Style

### Indentation and Formatting

- Use **2 spaces** for indentation (no tabs)
- Maximum line length: **100 characters**
- Use consistent formatting throughout the codebase
- Configure and use a code formatter (e.g., Prettier)

### Spacing

- Add space after keywords: `if (condition)`
- Add space around operators: `a + b`, `x === y`
- No space before function parentheses for function calls: `doSomething()`
- Add space before opening braces: `if (condition) {`

### Braces

- Always use braces for control statements, even for single-line blocks
- Opening brace on the same line (K&R style)

```javascript
// Good
if (condition) {
  doSomething();
}

// Bad
if (condition) doSomething();

if (condition)
{
  doSomething();
}
```

### Semicolons

- Use semicolons to terminate statements
- Be consistent with semicolon usage across the project

### Quotes

- Use single quotes `'` for strings by default
- Use backticks `` ` `` for template literals
- Be consistent throughout the project

```javascript
const message = 'Hello, World!';
const greeting = `Hello, ${name}!`;
```

### Arrow Functions

- Use arrow functions for anonymous functions and callbacks
- Omit parentheses for single parameters (unless using TypeScript types)
- Use implicit return for single expressions

```javascript
// Good
const double = num => num * 2;
const add = (a, b) => a + b;

items.map(item => item.name);

// With block
const process = data => {
  const result = transform(data);
  return result;
};
```

### Destructuring

- Use destructuring for objects and arrays when appropriate
- Improves readability and reduces redundant code

```javascript
// Good
const { name, email } = user;
const [first, second] = items;

// Instead of
const name = user.name;
const email = user.email;
```

### Modern JavaScript Features

- Use `const` and `let` instead of `var`
- Prefer `const` by default, use `let` only when reassignment is needed
- Use template literals for string interpolation
- Use spread operator for array/object manipulation
- Use async/await over promise chains

```javascript
// Good
const config = { ...defaultConfig, ...userConfig };
const newArray = [...oldArray, newItem];

async function fetchData() {
  const response = await fetch(url);
  return response.json();
}
```

## Comments and Documentation

### General Guidelines

- Write self-documenting code that needs minimal comments
- Use comments to explain "why", not "what"
- Keep comments up to date with code changes
- Remove commented-out code; use version control instead

### Inline Comments

```javascript
// Good - explains why
// Using setTimeout to debounce rapid consecutive calls
setTimeout(handleClick, 300);

// Bad - explains what (obvious from code)
// Increment counter by 1
counter++;
```

### Function Documentation

Use JSDoc style comments for functions:

```javascript
/**
 * Calculates the total price including tax
 * @param {number} price - The base price
 * @param {number} taxRate - The tax rate as a decimal (e.g., 0.1 for 10%)
 * @returns {number} The total price including tax
 */
function calculateTotal(price, taxRate) {
  return price * (1 + taxRate);
}
```

### TODO Comments

- Use TODO comments for planned improvements
- Include issue number or assignee when possible

```javascript
// TODO: Add input validation (#123)
// TODO(john): Optimize this query
```

## Testing

### Test Organization

- Write tests for all new features and bug fixes
- Organize tests to mirror source structure
- Use descriptive test names that explain what is being tested

### Test Naming

```javascript
describe('UserService', () => {
  describe('createUser', () => {
    it('should create a new user with valid data', () => {
      // test implementation
    });

    it('should throw an error when email is invalid', () => {
      // test implementation
    });
  });
});
```

### Test Coverage

- Aim for high test coverage (80%+ recommended)
- Focus on critical paths and edge cases
- Don't sacrifice quality for coverage percentage

### Arrange-Act-Assert Pattern

```javascript
it('should calculate the correct total', () => {
  // Arrange
  const price = 100;
  const taxRate = 0.1;

  // Act
  const result = calculateTotal(price, taxRate);

  // Assert
  expect(result).toBe(110);
});
```

## Error Handling

### Error Messages

- Provide clear, actionable error messages
- Include context about what went wrong
- Log errors appropriately

```javascript
// Good
throw new Error('Failed to fetch user data: Invalid user ID provided');

// Bad
throw new Error('Error');
```

### Try-Catch Blocks

- Use try-catch for operations that may fail
- Handle errors at the appropriate level
- Don't catch errors you can't handle

```javascript
async function fetchUserData(userId) {
  try {
    const response = await fetch(`/api/users/${userId}`);
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    return await response.json();
  } catch (error) {
    logger.error('Failed to fetch user data', { userId, error });
    throw error;
  }
}
```

### Validation

- Validate inputs early
- Use guard clauses to handle edge cases
- Provide meaningful validation messages

```javascript
function processPayment(amount, currency) {
  if (!amount || amount <= 0) {
    throw new Error('Amount must be a positive number');
  }
  if (!currency || !SUPPORTED_CURRENCIES.includes(currency)) {
    throw new Error(`Unsupported currency: ${currency}`);
  }
  // process payment
}
```

## Security

### Input Validation

- Always validate and sanitize user inputs
- Use allowlists over denylists when possible
- Validate on both client and server side

### Sensitive Data

- Never commit secrets, API keys, or passwords
- Use environment variables for configuration
- Sanitize logs to prevent leaking sensitive information

### Dependencies

- Keep dependencies up to date
- Regularly audit for security vulnerabilities
- Use only trusted, well-maintained packages

### SQL and Injection Prevention

- Use parameterized queries or ORMs
- Never construct queries with string concatenation
- Validate and escape all user inputs

## Linting and Formatting

### Tools

Configure and use appropriate linting and formatting tools:
- ESLint for JavaScript/TypeScript
- Prettier for code formatting
- EditorConfig for consistent editor settings

### Pre-commit Hooks

- Use pre-commit hooks to enforce code quality
- Run linters and formatters before commits
- Ensure tests pass before pushing

## Continuous Improvement

These conventions are living documents and should evolve with the project:
- Suggest improvements through pull requests
- Discuss major changes with the team
- Update conventions based on lessons learned

## References

- [JavaScript Style Guide](https://github.com/airbnb/javascript)
- [Clean Code principles](https://github.com/ryanmcdermott/clean-code-javascript)
- [SOLID Principles](https://en.wikipedia.org/wiki/SOLID)

---

Following these conventions helps maintain a high-quality, maintainable codebase. When in doubt, consistency with existing code is preferred.
