# Code Style Guidelines

## Overview

Consistent, readable PHP code focused on functionality over elegance. Dark theme UI with reusable classes. Maximum 100 lines of new code per lesson.

---

## PHP Code Standards

### File Structure

#### Section 1: Simple & Direct

```php
<?php
/**
 * Social Platform - Chapter X, Lesson X.X
 * [Brief file purpose]
 */

// Include shared components
require_once 'config.php';
session_start();

// Main functionality (keep under 100 lines)
// Clear comments explaining PHP concepts
?>
```

#### Section 2: Professional Structure

```php
<?php
declare(strict_types=1);

namespace SocialPlatform\Controllers;

use SocialPlatform\Models\User;

class UserController
{
    // Professional implementation
}
?>
```

### Naming Conventions

```php
// Variables: snake_case (matches database columns)
$user_name = 'john_doe';        // Good
$user_posts = [];               // Good
$is_logged_in = true;          // Good

// Functions: Section 1 - descriptive
function get_user_posts($user_id) { }      // Learning focus
function validate_email($email) { }       // Clear purpose

// Functions: Section 2 - professional
function getUserPosts(int $userId): array { }    // Type hints
function validateEmail(string $email): bool { }  // Return types

// Classes: PascalCase (Section 2)
class PostController { }
class UserRepository { }

// Constants: UPPER_SNAKE_CASE
const MAX_FILE_SIZE = 2097152;
const DATABASE_HOST = 'localhost';
```

### Code Formatting

```php
<?php
// 4 spaces indentation, no tabs
if ($user_logged_in) {
    echo "Welcome!";

    if ($has_messages) {
        display_messages();
    }
}

// Spaces around operators
$total = $price + $tax;

// Space after commas
function calculate($price, $tax, $discount) { }

// Braces on same line
if ($condition) {
    // code
} else {
    // code
}

foreach ($posts as $post) {
    // process post
}
?>
```

---

## Dark Theme CSS Standards

### Shared CSS Per Chapter

```css
/* Chapter X - styles.css (shared across all lessons) */

/* Base Theme */
body {
    background: #1a1a1a;
    color: #ccc;
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
}

/* Layout Components */
.container {
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
}

.card {
    background: #2a2a2a;
    padding: 20px;
    margin: 15px 0;
    border-radius: 5px;
}

.flex {
    display: flex;
    align-items: center;
    gap: 10px;
}

/* Typography */
.title {
    color: #fff;
    font-size: 1.4rem;
    margin-bottom: 10px;
}

.text {
    color: #ccc;
    line-height: 1.5;
}

.muted {
    color: #888;
    font-size: 0.9rem;
}

/* Interactive Elements */
.btn {
    padding: 10px 20px;
    background: #444;
    color: #fff;
    border: none;
    border-radius: 3px;
    cursor: pointer;
    text-decoration: none;
    display: inline-block;
}

.btn-primary {
    background: #007acc;
}

.btn:hover {
    opacity: 0.9;
}

/* Forms */
.form-group {
    margin-bottom: 15px;
}

.label {
    display: block;
    color: #ccc;
    margin-bottom: 5px;
}

.input {
    width: 100%;
    padding: 10px;
    background: #333;
    color: #fff;
    border: 1px solid #555;
    border-radius: 3px;
    box-sizing: border-box;
}

.input:focus {
    border-color: #007acc;
    outline: none;
}

/* Platform Components */
.post-card {
    background: #2a2a2a;
    padding: 15px;
    margin: 10px 0;
    border-radius: 5px;
}

.post-header {
    margin-bottom: 10px;
}

.post-title {
    color: #fff;
    font-size: 1.2rem;
    margin: 0;
}

.post-meta {
    color: #888;
    font-size: 0.9rem;
}

.user-avatar {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background: #444;
}

/* Navigation */
.nav {
    background: #333;
    padding: 10px 0;
}

.nav-link {
    color: #ccc;
    text-decoration: none;
    padding: 10px 15px;
    display: inline-block;
}

.nav-link:hover {
    color: #fff;
    background: #444;
}

/* Utility Classes */
.text-center { text-align: center; }
.text-right { text-align: right; }
.hidden { display: none; }
.error { color: #ff6b6b; }
.success { color: #51cf66; }
```

### CSS Class Usage Rules

```html
<!-- Use existing classes, don't create new ones -->
<div class="card">                     <!-- Good: Reusable -->
    <h2 class="title">Post Title</h2>
    <p class="text">Post content...</p>
    <div class="post-meta muted">
        By Username on Date
    </div>
</div>

<!-- Avoid creating specific classes -->
<div class="post-card-with-image">     <!-- Bad: Too specific -->
<div class="blue-title-large">         <!-- Bad: Not reusable -->
```

---

## HTML Standards

### Structure Pattern

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Social Platform</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <nav class="nav">
        <!-- Navigation using existing classes -->
    </nav>

    <main class="container">
        <div class="card">
            <!-- Content using existing classes -->
        </div>
    </main>
</body>
</html>
```

### Form Standards

```html
<form class="card" method="post">
    <h2 class="title">Form Title</h2>

    <div class="form-group">
        <label class="label" for="username">Username:</label>
        <input class="input" type="text" id="username" name="username" required>
        <?php if (isset($errors['username'])): ?>
            <div class="error"><?php echo htmlspecialchars($errors['username']); ?></div>
        <?php endif; ?>
    </div>

    <button class="btn btn-primary" type="submit">Submit</button>
</form>
```

---

## Comment Standards

### Section 1: Educational Comments

```php
<?php
// Connect to the social platform database
// PDO is PHP's secure way to work with databases
$pdo = new PDO($dsn, $username, $password);

// Get posts with user information in one query
// JOIN connects the posts and users tables
$sql = "SELECT p.*, u.username 
        FROM posts p 
        JOIN users u ON p.user_id = u.id 
        ORDER BY p.created_at DESC";

$stmt = $pdo->prepare($sql);
$stmt->execute();

// Get all results as an array
$posts = $stmt->fetchAll(PDO::FETCH_ASSOC);

// Display each post safely
foreach ($posts as $post) {
    // htmlspecialchars prevents XSS attacks
    echo "<h3>" . htmlspecialchars($post['title']) . "</h3>";
}
?>
```

### Section 2: Professional Comments

```php
<?php
/**
 * Retrieves posts with pagination and user data
 * 
 * @param int $page Page number (1-based)
 * @param int $limit Posts per page
 * @return array Posts with user information
 */
public function getPaginatedPosts(int $page = 1, int $limit = 10): array
{
    $offset = ($page - 1) * $limit;

    $sql = "SELECT p.*, u.username, u.avatar_url 
            FROM posts p 
            JOIN users u ON p.user_id = u.id 
            ORDER BY p.created_at DESC 
            LIMIT :limit OFFSET :offset";

    $stmt = $this->db->prepare($sql);
    $stmt->bindValue(':limit', $limit, PDO::PARAM_INT);
    $stmt->bindValue(':offset', $offset, PDO::PARAM_INT);
    $stmt->execute();

    return $stmt->fetchAll(PDO::FETCH_ASSOC);
}
?>
```

---

## Security Standards

### Input Handling

```php
// Always validate and sanitize
function validate_username($username) {
    $username = trim($username);

    if (strlen($username) < 3 || strlen($username) > 50) {
        return false;
    }

    if (!preg_match('/^[a-zA-Z0-9_]+$/', $username)) {
        return false;
    }

    return true;
}

// Always escape output
echo htmlspecialchars($user_input, ENT_QUOTES, 'UTF-8');

// Always use prepared statements
$stmt = $pdo->prepare("SELECT * FROM users WHERE id = ?");
$stmt->execute([$user_id]);
```

---

## Database Standards

### Table Design

```sql
-- Consistent naming: plural, snake_case
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL UNIQUE,
    email VARCHAR(255) NOT NULL UNIQUE,
    password_hash VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE posts (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    content TEXT,
    image_url VARCHAR(500),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,

    FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);
```

### Query Style

```sql
-- Simple, readable queries for Section 1
SELECT u.username, p.content, p.created_at
FROM posts p
JOIN users u ON p.user_id = u.id
WHERE p.id = ?
ORDER BY p.created_at DESC;

-- Complex queries with proper formatting for Section 2
SELECT 
    p.id,
    p.content,
    p.created_at,
    u.username,
    COUNT(l.id) as like_count
FROM posts p
    JOIN users u ON p.user_id = u.id
    LEFT JOIN likes l ON p.id = l.post_id
WHERE p.created_at >= DATE_SUB(NOW(), INTERVAL 7 DAY)
GROUP BY p.id
ORDER BY like_count DESC, p.created_at DESC
LIMIT 20;
```

---

## JavaScript Standards

### Section 1: Simple & Clear

```javascript
// Basic AJAX for social features
function likePost(postId) {
    const button = document.getElementById('like-btn-' + postId);
    button.textContent = 'Loading...';

    fetch('api/like-post.php', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ post_id: postId })
    })
    .then(response => response.json())
    .then(data => {
        if (data.success) {
            button.textContent = data.is_liked ? 'Unlike' : 'Like';
        }
    })
    .catch(error => {
        console.error('Error:', error);
        button.textContent = 'Error';
    });
}
```

---

## File Organization

```
chapter-X/
├── styles.css (shared across all lessons)
├── config.php (database connection)
├── functions.php (shared functions)
└── lesson-files/
    ├── index.php
    ├── login.php
    └── profile.php
```

This style guide ensures consistent, readable code while keeping design minimal and functionality-focused.
