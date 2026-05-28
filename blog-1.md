Blog 1: Why any is a Type Safety Hole and Why unknown is Safer
Introduction

TypeScript is designed to help developers write safer and more reliable code through static type checking. However, not all types provide the same level of safety. Two commonly discussed types are any and unknown. While both can represent values of any type, they behave very differently. Understanding these differences and the concept of type narrowing is essential for writing maintainable TypeScript applications.

What is any?

The any type tells TypeScript to completely ignore type checking for a variable. Once a value is assigned the any type, the compiler allows any operation on it without producing errors.

let userInfo: any = "Hello World";

userInfo = 123;
userInfo = true;

console.log(userInfo.toUpperCase()); // No compile-time error

In the example above, TypeScript does not verify whether toUpperCase() exists on the current value. This can lead to unexpected runtime errors.

Why is any Called a "Type Safety Hole"?

The term "type safety hole" is used because any bypasses TypeScript's type-checking system. It creates a gap where errors can enter the application unnoticed.

let number: any = 100;

console.log(number.toUpperCase());

The code compiles successfully, but at runtime it throws an error because numbers do not have a toUpperCase() method.

Using any extensively defeats the main purpose of TypeScript, which is preventing such mistakes before the code runs.

What is unknown?

The unknown type is a safer alternative to any. It can hold any value, but TypeScript does not allow operations on it until its type is verified.

let Information: unknown = "TypeScript";

console.log(Information.toUpperCase()); // Error

TypeScript immediately reports an error because it does not know whether data is actually a string.

This extra restriction encourages developers to validate data before using it.

Why is unknown Safer?

When working with external data such as API responses, user input, or third-party libraries, the exact data type may not be known in advance.

let response: unknown = "Hello Developer";

Before using the value, we must check its type.

if (typeof response === "string") {
    console.log(response.toUpperCase());
}

This prevents many common runtime errors and makes the code more reliable.

Understanding Type Narrowing

Type narrowing is the process of reducing a broad type into a more specific type through checks and conditions.

Consider the following example:

let value: unknown = "Learning TypeScript";

if (typeof value === "string") {
    console.log(value.length);
}

Initially, value is of type unknown. After the typeof check, TypeScript narrows its type to string within the if block.

Common Ways to Narrow Types
Using typeof
let data: unknown = 42;

if (typeof data === "number") {
    console.log(data.toFixed(2));
}
Using instanceof
let dateValue: unknown = new Date();

if (dateValue instanceof Date) {
    console.log(dateValue.getFullYear());
}
Using Custom Type Guards
function isString(value: unknown): value is string {
    return typeof value === "string";
}

let text: unknown = "Type Guard Example";

if (isString(text)) {
    console.log(text.toUpperCase());
}
When Should You Use any?

any should be used sparingly, mainly in situations such as:

Migrating large JavaScript projects to TypeScript.
Working with legacy code.
Temporary development situations where type definitions are unavailable.

Even in these cases, replacing any with proper types later is recommended.

When Should You Use unknown?

Use unknown whenever data comes from uncertain sources, such as:

API responses
User input
Local storage
Third-party libraries

It forces validation before usage and maintains TypeScript's safety guarantees.

Conclusion

Although both any and unknown can store values of any type, they serve different purposes. The any type disables TypeScript's safety checks and can introduce hidden bugs, making it a "type safety hole." On the other hand, unknown preserves type safety by requiring developers to verify a value's type before using it. Through type narrowing, TypeScript can safely determine the correct type and help prevent runtime errors. Therefore, whenever possible, unknown should be preferred over any for handling unpredictable data.