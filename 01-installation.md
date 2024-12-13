---
layout: page
title: Installation & Setup
permalink: /installation/
menu: true
---

# Quick Installation Guide

## System Requirements

- PHP 7+ 
- Apache/Nginx
- mysqli extension
- MariaDB/MySQL (optional but recommended)

## Installation Methods

### 1. Quick Start (Recommended)

```bash
# Download and setup
wget http://github.com/mintyphp/mintyphp/archive/v3.0.4.zip
unzip mintyphp-3.0.4.zip
cd mintyphp-3.0.4

# Start development server
bash start.sh
```

### 2. Composer Installation

```bash
composer create-project mintyphp/mintyphp myapp
cd myapp
php -S localhost:8000 -t web/
```

## Configuration

1. Visit http://localhost:8000/
2. Enter database credentials in the configurator
3. Test connection and save

## Example Database Setup

```sql
-- Create a simple users table
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL UNIQUE,
    password_hash VARCHAR(255) NOT NULL,
    active TINYINT(1) DEFAULT 1
);
```

## Apache Configuration 

Create .htaccess in web/:

```apache
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^ index.php [QSA,L]
```

## Nginx Configuration

```nginx
location / {
    try_files $uri $uri/ /index.php?$query_string;
}
```

## Troubleshooting

1. Ensure correct file permissions
2. Check PHP extensions
3. Verify database connectivity
4. Enable error reporting in development

Your MintyPHP app should now be running at http://localhost:8000/
