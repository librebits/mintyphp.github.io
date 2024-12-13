---
layout: page
title: API Reference
permalink: /api/
menu: true
---

# MintyPHP API Reference

## Database Operations

### Query Functions

```php
// Select multiple rows
$users = DB::select("SELECT * FROM users WHERE active = ?", 1);

// Select single row
$user = DB::selectOne("SELECT * FROM users WHERE id = ?", $userId);

// Select single value
$count = DB::selectValue("SELECT COUNT(*) FROM users");

// Select key-value pairs
$usernames = DB::selectPairs("SELECT id, username FROM users");

// Select column values
$emails = DB::selectValues("SELECT email FROM users");
```

### Modification Functions

```php
// Insert record
$id = DB::insert("INSERT INTO users (username, email) VALUES (?, ?)", 
    $username, $email);

// Update records
$affected = DB::update("UPDATE users SET active = ? WHERE last_login < ?", 
    0, $date);

// Delete records
$removed = DB::delete("DELETE FROM users WHERE inactive = 1");
```

## HTTP Client

### Curl Operations

```php
// GET request
$data = Curl::call('GET', 'https://api.example.com/users');

// POST request with data
$response = Curl::call('POST', 'https://api.example.com/users', [
    'name' => 'John',
    'email' => 'john@example.com'
]);

// API navigation (follows redirects)
$page = Curl::navigate('GET', 'https://example.com/page');
```

## Authentication

### User Management

```php
// Login user
if (Auth::login($username, $password)) {
    Router::redirect('/dashboard');
}

// Register user
if (Auth::register($username, $password)) {
    Flash::set('success', 'Registration successful');
}

// Logout user
Auth::logout();
```

## Flash Messages

```php
// Set flash message
Flash::set('success', 'Profile updated');
Flash::set('error', 'Invalid input');

// Get all flash messages
$messages = Flash::get();
```

## Routing

```php
// Add custom route
Router::addRoute('/', '/home');
Router::addRoute('/blog/{id}', '/blog/view');

// Redirect response
Router::redirect('/login');

// JSON response
Router::json(['status' => 'success', 'data' => $result]);
```

## Security

### CSRF Protection

```php
// In your form template:
<form method="post">
    <?= Session::getCsrfInput() ?>
    <!-- form fields -->
</form>
```

### Output Escaping

```php
// In your template:
<div class="user-info">
    <h1><?= e($user['name']) ?></h1>
    <p><?= e($user['bio']) ?></p>
</div>
```

## Template Buffering

```php
// Start capturing output
Buffer::start('sidebar');
?>
    <div class="sidebar">
        <!-- sidebar content -->
    </div>
<?php
Buffer::end('sidebar');

// Get captured content
$sidebarContent = Buffer::get('sidebar');

// Set content directly
Buffer::set('title', 'Dashboard');
```

## Debugging

```php
// Debug variable
d($variable);  // Shows in debug toolbar

// Debug database queries
d(DB::$queries);  // Shows all executed queries
```

## Complete Function Reference

| Function | Purpose | Example |
|----------|----------|----------|
| `e($str)` | Escape output | `<?= e($user['name']) ?>` |
| `d($var)` | Debug variable | `d($results)` |
| `DB::select()` | Query rows | `DB::select("SELECT * FROM users")` |
| `Auth::login()` | Login user | `Auth::login($user, $pass)` |
| `Flash::set()` | Set message | `Flash::set('info', 'Updated')` |
| `Router::redirect()` | Redirect | `Router::redirect('/home')` |
| `Session::getCsrfInput()` | CSRF token | `<?= Session::getCsrfInput() ?>` |
| `Buffer::start()` | Start capture | `Buffer::start('content')` |

Remember to always:
1. Escape user output with `e()`
2. Use parameterized queries
3. Include CSRF protection in forms
4. Set appropriate flash messages
5. Handle errors gracefully
