# PHP Array Spread Operator (`...`)

The **array spread operator** (`...`) in PHP is a powerful and clean way to merge or unpack arrays. Introduced in PHP 7.4 for arrays, it makes working with multiple arrays simpler and more readable.

---

## What Is the Spread Operator?

The spread operator (`...`) is used to **unpack** values from an array into another array.

> ✅ Available from **PHP 7.4+** for arrays.

---

## Basic Syntax

```php
$array1 = [1, 2, 3];
$array2 = [...$array1, 4, 5];

// Result: [1, 2, 3, 4, 5]
```


## Use Cases

1. Merging Arrays
```php
$a = [1, 2];
$b = [3, 4];
$c = [...$a, ...$b];

// [1, 2, 3, 4]

//-  Note: Only works with numeric-keyed arrays. Associative keys are ignored when duplicated.

```

2. Passing Arrays to Functions
   
```php
function sum($a, $b, $c) {
    return $a + $b + $c;
}

$args = [1, 2, 3];

echo sum(...$args); // 6

```

3. Combining Arrays with New Values
```php
$defaults = ['host' => 'localhost', 'port' => 3306];
$custom = ['port' => 3307];

$config = [...$defaults, ...$custom];

// ['host' => 'localhost', 'port' => 3307]
//- Later values override earlier ones when keys match.
```

___

## Limitations

- -Only works with arrays, not Traversables (e.g., generators).
- Only works with integer keys and string keys. Duplicates will be overridden.
- Will throw an error if you try to spread a non-array.
