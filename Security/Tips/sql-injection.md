# 🛡️ Prepared Statements to Prevent SQL Injection Attacks

SQL injection is one of the most common and dangerous vulnerabilities in web applications, allowing attackers to manipulate database queries.  
Prepared Statements are a secure way to execute SQL queries by separating the query structure from user input, effectively preventing SQL injection attacks.

هجمات SQL Injection من أخطر الثغرات في تطبيقات الويب، لأنها بتسمح للمهاجمين يعبثوا في استفسارات قاعدة البيانات.  
الـ Prepared Statements هي طريقة آمنة لتنفيذ الاستفسارات بفصل بنية الاستفسارة عن البيانات اللي بيبعتها المستخدم.

<hr>

## What is SQL Injection? 

- SQL Injection occurs when an attacker injects malicious SQL code into a query through user input, potentially allowing them to read, modify, or delete database data.  

- هجمات SQL Injection بتحصل لما المهاجم يحط كود SQL مضر في الحقول اللي بيبعتها (زي اسم المستخدم أو الباسورد)، وده ممكن يخليه يتحكم في الداتابيز.

#### ❌ Vulnerable Code 

```php
$username = $_POST['username'];
$password = $_POST['password'];
$query = "SELECT * FROM users WHERE username = '$username' AND password = '$password'";
$result = mysqli_query($conn, $query);

// If an attacker inputs username as ' OR '1'='1 and password as ', the query becomes:
SELECT * FROM users WHERE username = '' OR '1'='1' AND password = ''

//ده بيخلّي المهاجم يدخل من غير باسورد صحيح

```

<hr>

## What Are Prepared Statements?

- Prepared statements are precompiled SQL queries with placeholders (? or :name) for user inputs.
- They ensure user data is treated as data only, not executable SQL.

- الجمل المُعدة مسبقًا هي استفسارات SQL بتتجهز مسبقًا باستخدام أماكن مؤقتة للبيانات، وده بيخلي الداتابيز تتعامل مع البيانات كـ بيانات فقط، مش كود يتنفذ.

## How They Work?

- Prepare — The SQL query is compiled with placeholders.
- Bind — User input is safely bound to the placeholders.
- Execute — The query runs with bound data, eliminating injection risks.

<hr>

## Using Prepared Statements in PHP

### Example using PDO

```php
try {
    // Connect to the database
    $pdo = new PDO("mysql:host=localhost;dbname=mydb", "username", "password");
    $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

    // Prepare the query with placeholders
    $stmt = $pdo->prepare("SELECT * FROM users WHERE username = ? AND password = ?");
    
    // Bind user input to placeholders
    $username = $_POST['username'];
    $password = $_POST['password'];
    $stmt->execute([$username, $password]);
    
    // Fetch the result
    $user = $stmt->fetch(PDO::FETCH_ASSOC);
    
    if ($user) {
        echo "Login successful!";
    } else {
        echo "Invalid credentials.";
    }
} catch (PDOException $e) {
    echo "Error: " . $e->getMessage();
}

```

<hr>

## Why Use Prepared Statements?

- Prevents SQL Injection — Separates query logic from input.
- Improved Security — Inputs are auto-sanitized.
- Reusability — You can execute the same statement with different values.
- Database Agnostic — Especially with PDO, it works across many databases.

## Practical Example

```php
try {
    $pdo = new PDO("mysql:host=localhost;dbname=mydb", "username", "password");
    $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

    // Prepare the query with named parameters
    $stmt = $pdo->prepare("SELECT * FROM users WHERE username = :username AND password = :password");
    
    // Bind values to named parameters
    $stmt->bindParam(':username', $_POST['username']);
    $stmt->bindParam(':password', $_POST['password']);
    
    // Execute the query
    $stmt->execute();
    
    // Fetch the result
    $user = $stmt->fetch(PDO::FETCH_ASSOC);
    
    if ($user) {
        echo "Login successful!";
    } else {
        echo "Invalid credentials.";
    }
} catch (PDOException $e) {
    echo "Error: " . $e->getMessage();
}
```
