# ⚙️ PHP: `declare(strict_types=1);`

`declare(strict_types=1);` is a directive in PHP that enforces **strict type checking** on scalar type hints and return types. When enabled, PHP will no longer perform type juggling and will throw a `TypeError` if a value of the wrong type is passed or returned.

<hr>

## 🔍 Why Use It?

- Prevents hidden bugs.
- Enforces strict code standards.
- Improves reliability in large-scale applications.
- Makes your intent clear: types *must* match.

<hr>

## 🧪 Basic Example

```php
declare(strict_types=1);

function add(int $a, int $b): int {
    return $a + $b;
}

echo add(5, 10);      // ✅ OK
echo add("5", "10");  // ❌ Throws TypeError

//- Without strict_types=1, PHP would have converted "5" and "10" to integers automatically

```

<hr>

## 🚀 Advanced Examples

1. Function Return Type

```php
declare(strict_types=1);

function multiply(float $a, float $b): float {
    return $a * $b;
}

echo multiply(5, 2);      // ✅ OK
echo multiply(5, "2");    // ❌ TypeError

```
2. With Classes

```php
declare(strict_types=1);

class User {
    public string $name;
    public function __construct(string $name) {
        $this->name = $name;
    }
}

function greet(User $user): string {
    return "Hello, " . $user->name;
}

$user = new User("Hesham");
echo greet($user);       // ✅ OK
echo greet("NotAUser");  // ❌ TypeError

```

3. Type Hints for Arrays
   
```php
declare(strict_types=1);

function getNames(array $names): array {
    return array_map(fn($n) => strtoupper($n), $names);
}

print_r(getNames(["ahmed", "hesham"]));  // ✅ OK
print_r(getNames("hesham"));             // ❌ TypeError

```

4. In Classes with Setters

```php
declare(strict_types=1);

class Product {
    private int $price;

    public function setPrice(int $price): void {
        $this->price = $price;
    }
}

$product = new Product();
$product->setPrice(100);      // ✅ OK
$product->setPrice("100");    // ❌ TypeError

```

<hr>

## ✅ Best Practices
- Always place declare(strict_types=1); at the top of the file.
- Use in all files consistently in modern projects.
- Pair with static analysis tools like PHPStan or Psalm.

<hr>

**Want cleaner, safer PHP code? Use declare(strict_types=1); at the top of your files and let the types do their job.**

