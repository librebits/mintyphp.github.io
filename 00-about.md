---
layout: page
title: About MintyPHP
permalink: /
---

# MintyPHP: A Pragmatic PHP Framework

MintyPHP is a lightweight, security-focused PHP framework that embraces simplicity. Unlike complex frameworks, it follows a practical approach:

## Core Philosophy

1. **One Variable Scope**: All layers share the same scope for straightforward debugging
2. **Direct SQL**: Write your own queries without ORM overhead
3. **Native PHP Templates**: Use PHP's built-in templating power

## Quick Example

```php
// Action file (pages/users.php)
$users = DB::select("SELECT * FROM users WHERE active = ?", 1);

// View file (pages/users.phtml)
<h1>Active Users</h1>
<ul>
<?php foreach ($users as $user): ?>
    <li><?= e($user['name']) ?></li> <!-- XSS protection with e() -->
<?php endforeach; ?>
</ul>
```

## Security Features

- Built-in XSS protection via `e()` function
- CSRF protection via `Session::getCsrfInput()`
- SQL injection prevention through parameterized queries
- Integrated firewall for DDoS protection

## Latest Release: v3.0.4

Get started with MintyPHP:

- [Download Latest Release](http://github.com/mintyphp/mintyphp/archive/v3.0.4.zip)
- [GitHub Repository](https://github.com/mintyphp/mintyphp)
- [Documentation](/docs)

## Recent Updates

- MintyPHP v3 release with enhanced security features
- Now available on Packagist for easy Composer installation
- Simplified mental model for rapid development
