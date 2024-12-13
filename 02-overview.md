---
layout: page
title: Framework Overview
permalink: /overview/
menu: true
---

# MintyPHP Framework Overview

## Directory Structure

```
myapp/
├── pages/           # Views & Actions
│   ├── home.phtml   # View file
│   └── home.php     # Action file
├── web/            # Public files
│   └── index.php   # Front controller
└── templates/      # Layout templates
```

## Practical Examples

### 1. Basic Page with Database

```php
// pages/products.php (Action)
$category = isset($_GET['cat']) ? $_GET['cat'] : 'all';
$products = DB::select("
    SELECT * FROM products 
    WHERE category = ? 
    ORDER BY name", $category
);

// pages/products.phtml (View)
<h1>Products: <?= e($category) ?></h1>
<div class="grid">
    <?php foreach($products as $product): ?>
        <div class="product">
            <h3><?= e($product['name']) ?></h3>
            <p><?= e($product['description']) ?></p>
            <span>$<?= e($product['price']) ?></span>
        </div>
    <?php endforeach; ?>
</div>
```

### 2. API Integration

```php
// pages/weather.php
$city = $_GET['city'] ?? 'Amsterdam';
$weather = Curl::call('GET', 
    "https://api.weather.com/v1/current?city=" . urlencode($city)
);

// pages/weather.phtml
<div class="weather-widget">
    <h2><?= e($city) ?> Weather</h2>
    <p>Temperature: <?= e($weather['temp']) ?>°C</p>
    <p>Conditions: <?= e($weather['conditions']) ?></p>
</div>
```

### 3. Authentication Example

```php
// pages/login.php
if ($_POST) {
    if (Auth::login($_POST['username'], $_POST['password'])) {
        Router::redirect('/dashboard');
    }
    Flash::set('error', 'Invalid credentials');
}

// pages/login.phtml
<form method="post">
    <?= Session::getCsrfInput() ?>
    <input name="username" required>
    <input type="password" name="password" required>
    <button>Login</button>
</form>
```

## Security Features

- XSS Prevention: Always use `e()` in views
- CSRF Protection: Include `Session::getCsrfInput()`
- SQL Injection: Use parameterized queries
- Rate Limiting: Built-in firewall

## Debugging

Access the debug toolbar at `http://localhost:8000/?debug=1` to see:

- SQL queries
- API calls
- Session data
- Request/Response info

Remember: MintyPHP aims for simplicity and security while maintaining high performance.
