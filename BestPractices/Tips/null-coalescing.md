# ❓ the Null Coalescing Operator (`??`) in PHP

The **Null Coalescing Operator (`??`)** in PHP is a concise way to handle `null` values and undefined variables. Introduced in **PHP 7.0**, it helps developers write cleaner and more readable code when working with optional data.

<hr>

## 🔍 What is the Null Coalescing Operator?

The `??` operator checks whether a variable exists **and** is not `null`. If it does, it returns its value. If not, it returns a default value specified after the operator.

<hr>

## ✅ Syntax

```php

$value = $variable ?? $default;

//- $variable: The variable or expression to check.
//- $default: The fallback value if $variable is null or not set.

```

<hr>

## 🛠️ How It Works
- ✅ If $variable exists and is not null, its value is returned.
- ❌ If $variable is null or not set, $default is returned.
- ⏹️ The evaluation short-circuits — it stops as soon as a non-null value is found.

<hr>

## 📦 Examples

1. Basic Usage

```php
$username = null;

// Without ??
$displayName = isset($username) ? $username : 'Guest';

// With ??
$displayName = $username ?? 'Guest';

echo $displayName; // Guest

```

2. Arrays

```php
$data = ['name' => 'John'];

$name = $data['name'] ?? 'Anonymous'; // John
$email = $data['email'] ?? 'no-email@example.com'; // no-email@example.com

```

3. Chaining

```php
$input = null;
$backup = null;
$default = 'Unknown';

$result = $input ?? $backup ?? $default;

echo $result; // Unknown

```

<hr>

## 🔁 Comparison With Other Operators

1. Ternary with isset()
   
```php
// Old way
$username = isset($_GET['user']) ? $_GET['user'] : 'Guest';

// With ??
$username = $_GET['user'] ?? 'Guest';

```

2. Null Coalescing Assignment (??=) — PHP 7.4+

```php
$username = null;
$username ??= 'Guest';

echo $username; // Guest

```
<hr>

## 🌟 Key Features
- ✅ Null Safety — avoids warnings on undefined values.
- ⚡ Short-circuit Evaluation — better performance.
- 📖 Readable Syntax — more expressive code.
- 🔐 Safe with Arrays — no need for isset() or array_key_exists().

<hr>

**The Null Coalescing Operator (??) is a powerful feature that should be in every PHP developer’s toolkit. It improves code readability, safety, and conciseness, especially when dealing with user input, configuration arrays, or optional values in APIs.**