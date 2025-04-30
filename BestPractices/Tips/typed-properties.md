# Typed Properties

Starting from **PHP 7.4**, the language introduced **Typed Properties**, allowing developers to declare the expected type of class properties. This improves code clarity, enables better static analysis, and helps catch bugs early.

<hr>

## 📌 What Are Typed Properties?

Typed Properties let you define the data type of class properties directly in the class body, similar to how you type method arguments and return values.

```php
class User {
    public int $id;
    public string $name;
    public bool $isActive;
}
```

## Benefits

- Improved Code Safety: Enforces type constraints automatically.
- Cleaner Code: Makes class structure self-documenting.
- Better Tooling: Enhances IDE support and static analysis.
- Fewer Bugs: Catches type mismatches at runtime.
  
<hr>

### Rules & Behavior

- You must initialize typed properties before reading them unless they are nullable.
- If a property is not initialized, accessing it throws an Error.

```php
class Product {
    public int $price;
}

$p = new Product();
echo $p->price; // ❌ Error: Typed property Product::$price must not be accessed before initialization

```

### Nullable Properties

```php
// Use ? to allow null values

class Product {
    public ?int $discount = null;
}

```

<hr>

## Supported Types

- Scalar types: int, float, string, bool
- Complex types: array, object, callable, iterable
- Class/interface names (e.g. User, DateTime)
- Nullable types (?Type)
- self, parent, static

## 🚫 Not Allowed
- Union types (until PHP 8.0+)
- Default values that don’t match the declared type
- Accessing uninitialized properties

<hr>

## Real-World Example

```php
class Post {
    public int $id;
    public string $title;
    public ?string $content;

    public function __construct(int $id, string $title, ?string $content = null) {
        $this->id = $id;
        $this->title = $title;
        $this->content = $content;
    }
}
```

> Typed properties bring strong typing to object properties in PHP, making your codebase more robust and easier to maintain. Adopt them wherever possible to benefit from type safety and clarity.