# PHP Fluent Function Interface

The **Fluent Function Interface** in PHP is a design approach that allows you to **chain method calls** together in a readable and elegant way. It enhances the developer experience and can lead to cleaner, more expressive code.

---

##  What Is a Fluent Interface?

A **fluent interface** is a style of object-oriented API that allows for method chaining by returning `$this` from each method.

### Example:

```php
$user->setName('John')
     ->setEmail('john@example.com')
     ->activate();

```

## How to Build a Fluent Interface in PHP

- Here’s a basic example
```php
class UserBuilder
{
    protected $data = [];

    public function setName(string $name): self
    {
        $this->data['name'] = $name;
        return $this;
    }

    public function setEmail(string $email): self
    {
        $this->data['email'] = $email;
        return $this;
    }

    public function activate(): self
    {
        $this->data['active'] = true;
        return $this;
    }

    public function get(): array
    {
        return $this->data;
    }
}

```
- Usage
```php
$user = (new UserBuilder())
            ->setName('Alice')
            ->setEmail('alice@example.com')
            ->activate()
            ->get();

```

___

## Benefits of Fluent Interfaces
- Readable syntax – code flows top-down naturally.
- Less repetition – no need to repeat the variable on every line.
- Flexible and modular – useful in builders, queries, configs, etc.
- Commonly used in modern PHP libraries and frameworks (like Laravel).

___

## Real-World Examples

```php
$users = DB::table('users')
            ->where('active', 1)
            ->orderBy('name')
            ->limit(10)
            ->get();

```

___

## Best Use Cases
- Builders (e.g., UserBuilder, QueryBuilder)
- Configuration chains
- APIs that require sequential setup steps

