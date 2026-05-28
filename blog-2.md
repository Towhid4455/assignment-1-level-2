Blog 2: How Pick and Omit Utility Types Keep Your Code DRY
Introduction

As applications grow, developers often need multiple versions of the same data structure. For example, a user registration form may require different fields than a user profile page. Writing separate interfaces for every situation can lead to code duplication and maintenance problems.

TypeScript provides utility types such as Pick and Omit to solve this problem. These utilities allow developers to create specialized versions of an existing interface while keeping their code DRY (Don't Repeat Yourself).

The Problem with Duplicate Interfaces

Consider a master interface representing a user.

interface User {
    id: number;
    name: string;
    email: string;
    password: string;
    role: string;
}

Suppose we create another interface for displaying public user information.

interface PublicUser {
    id: number;
    name: string;
    email: string;
}

Notice that several properties are repeated. If the User interface changes, we must update every related interface manually. This increases maintenance effort and the risk of inconsistencies.

What is Pick?

The Pick utility type creates a new type by selecting specific properties from an existing type.

Syntax
Pick<Type, Keys>
Example
interface User {
    id: number;
    name: string;
    email: string;
    password: string;
    role: string;
}

type PublicUser = Pick<User, "id" | "name" | "email">;

The resulting type becomes:

{
    id: number;
    name: string;
    email: string;
}

Instead of rewriting properties, we reuse the original interface.

Practical Use Case
type UserCard = Pick<User, "name" | "email">;

This type can be used for displaying user information on a profile card.

What is Omit?

The Omit utility type creates a new type by removing specific properties from an existing type.

Syntax
Omit<Type, Keys>
Example
interface User {
    id: number;
    name: string;
    email: string;
    password: string;
    role: string;
}

type UserWithoutPassword = Omit<User, "password">;

The resulting type becomes:

{
    id: number;
    name: string;
    email: string;
    role: string;
}

This is particularly useful when sensitive information should not be exposed.

Practical Use Case
type UserResponse = Omit<User, "password">;

When sending user data from a server, excluding the password helps improve security.

How Pick and Omit Prevent Code Duplication

Without utility types:

interface UserProfile {
    id: number;
    name: string;
    email: string;
}

With utility types:

type UserProfile = Pick<User, "id" | "name" | "email">;

The second approach references the original interface instead of duplicating properties. Any updates to the base interface automatically flow to derived types.

This reduces:

Repeated code
Maintenance effort
Human errors
Inconsistencies across the application
Keeping Code DRY (Don't Repeat Yourself)

The DRY principle encourages developers to avoid repeating the same information in multiple places.

Using Pick and Omit helps achieve DRY because:

The master interface remains the single source of truth.
Specialized types are generated automatically.
Changes are easier to manage.
Code becomes cleaner and more maintainable.
Example
interface Product {
    id: number;
    name: string;
    price: number;
    stock: number;
    supplierInfo: string;
}

type ProductCard = Pick<Product, "id" | "name" | "price">;

type PublicProduct = Omit<Product, "supplierInfo">;

Instead of creating multiple interfaces, we derive them directly from the main Product interface.

Best Practices
Use Pick when you need only a few properties.
Use Omit when you need most properties except a few.
Keep one master interface as the source of truth.
Avoid creating duplicate interfaces unnecessarily.
Conclusion

TypeScript's Pick and Omit utility types provide an elegant way to create specialized "slices" of a master interface. They reduce code duplication, simplify maintenance, and help developers follow the DRY principle. By deriving new types from existing ones, applications become more consistent, scalable, and easier to maintain. These utility types are essential tools for writing clean and professional TypeScript code.