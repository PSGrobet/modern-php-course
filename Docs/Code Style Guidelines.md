# Code Style Guidelines

## Overview

These guidelines ensure consistent, readable, and maintainable code across all lessons in both sections of the course. They reflect modern PHP best practices while being beginner-friendly.

---

## PHP Code Standards

### File Structure

#### Section 1 (Learning Path) - Simple Structure

```php
<?php
/**
 * Social Platform Project - Chapter X, Lesson X.X
 * [Brief description of file purpose]
 */

// Include configuration and dependencies
require_once 'config.php';
require_once 'functions.php';

// Session management (if needed)
session_start();

// Main functionality
// [Code implementation here]

// Include footer/cleanup if needed
?>
```

#### Section 2 (Builder's Path) - Professional Structure

```php
<?php
declare(strict_types=1);

/**
 * Social Platform Project - Professional Implementation
 * 
 * [Detailed class/file description]
 * 
 * @package SocialPlatform\[Namespace]
 * @author Course Student
 * @version 1.0
 */

namespace SocialPlatform\Controllers;

use SocialPlatform\Models\User;
use SocialPlatform\Services\AuthService;

class UserController
{
    // Class implementation
}
?>
```

### Naming Conventions

#### Variables

```php
// Use snake_case for variables (consistent with database columns)
$user_name = 'john_doe';           // Good
$user_posts = [];                  // Good
$is_logged_in = true;             // Good

$userName = 'john_doe';           // Bad (camelCase)
$usrNm = 'john_doe';             // Bad (abbreviations)
$data = [];                       // Bad (not descriptive)
```

#### Functions

```php
// Section 1: Simple, descriptive function names
function get_user_posts($user_id) {
    // Implementation
}

function validate_email($email) {
    // Implementation
}

function sanitize_input($input) {
    // Implementation
}

// Section 2: Professional naming with type hints
function getUserPosts(int $userId): array {
    // Implementation
}

function validateEmail(string $email): bool {
    // Implementation
}

function sanitizeInput(string $input): string {
    // Implementation
}
```

#### Classes (Section 2)

```php
// PascalCase for class names
class UserController { }           // Good
class PostRepository { }           // Good
class EmailService { }             // Good

class usercontroller { }           // Bad
class User_Controller { }          // Bad
class UC { }                       // Bad
```

#### Constants

```php
// UPPER_SNAKE_CASE for constants
define('MAX_FILE_SIZE', 2097152);        // Good
const DATABASE_HOST = 'localhost';       // Good

define('maxFileSize', 2097152);          // Bad
const databaseHost = 'localhost';        // Bad
```

### Code Formatting

#### Indentation and Spacing

```php
<?php
// Use 4 spaces for indentation (no tabs)
if ($user_is_logged_in) {
    echo "Welcome back!";

    if ($has_new_messages) {
        echo "You have new messages!";
    }
}

// Space around operators
$total = $price + $tax;              // Good
$total=$price+$tax;                  // Bad

// Space after commas
function calculate_total($price, $tax, $discount) {  // Good
function calculate_total($price,$tax,$discount) {    // Bad
```

#### Braces and Control Structures

```php
// Opening brace on same line for functions and classes
function get_user_posts($user_id) {
    // Implementation
}

class UserController {
    // Class content
}

// Control structures - opening brace on same line
if ($condition) {
    // Code
} elseif ($other_condition) {
    // Code
} else {
    // Code
}

// Loops
for ($i = 0; $i < count($posts); $i++) {
    // Code
}

foreach ($posts as $post) {
    // Code
}

while ($row = $stmt->fetch()) {
    // Code
}
```

### Comment Standards

#### Section 1 (Learning Path) - Educational Comments

```php
<?php
// Connect to the database
// We learned about PDO in Chapter 3
$pdo = new PDO($dsn, $username, $password);

// Get all posts from the database
// ORDER BY created_at DESC means newest posts first
$sql = "SELECT * FROM posts ORDER BY created_at DESC";
$stmt = $pdo->prepare($sql);
$stmt->execute();

// Fetch all results as an associative array
// This gives us an array where we can access columns by name
$posts = $stmt->fetchAll(PDO::FETCH_ASSOC);

// Loop through each post and display it
foreach ($posts as $post) {
    // Display the post title
    echo "<h3>" . htmlspecialchars($post['title']) . "</h3>";

    // Display the post content (limited to 200 characters)
    echo "<p>" . substr(htmlspecialchars($post['content']), 0, 200) . "...</p>";
}
?>
```

#### Section 2 (Builder's Path) - Professional Comments

```php
<?php
/**
 * Retrieves paginated posts with associated user data
 * 
 * This method joins posts with users table to get author information
 * and implements proper pagination for performance.
 * 
 * @param int $page Page number (1-based)
 * @param int $limit Number of posts per page
 * @return array Collection of posts with user data
 * @throws DatabaseException When database query fails
 */
public function getPaginatedPosts(int $page = 1, int $limit = 10): array
{
    $offset = ($page - 1) * $limit;

    // Use JOIN to get user data efficiently in single query
    $sql = "SELECT p.*, u.username, u.avatar_url 
            FROM posts p 
            JOIN users u ON p.user_id = u.id 
            WHERE p.is_published = 1 
            ORDER BY p.created_at DESC 
            LIMIT :limit OFFSET :offset";

    try {
        $stmt = $this->db->prepare($sql);
        $stmt->bindValue(':limit', $limit, PDO::PARAM_INT);
        $stmt->bindValue(':offset', $offset, PDO::PARAM_INT);
        $stmt->execute();

        return $stmt->fetchAll(PDO::FETCH_ASSOC);
    } catch (PDOException $e) {
        throw new DatabaseException("Failed to retrieve posts: " . $e->getMessage());
    }
}
?>
```

---

## HTML Standards

### Structure and Semantics

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Social Platform - Page Title</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
    <!-- Use semantic HTML5 elements -->
    <header class="site-header">
        <nav class="main-navigation">
            <!-- Navigation content -->
        </nav>
    </header>

    <main class="main-content">
        <article class="post">
            <header class="post-header">
                <h2 class="post-title">Post Title</h2>
                <div class="post-meta">
                    <span class="post-author">Author Name</span>
                    <time class="post-date" datetime="2024-01-15">January 15, 2024</time>
                </div>
            </header>
            <div class="post-content">
                <!-- Post content -->
            </div>
        </article>
    </main>

    <footer class="site-footer">
        <!-- Footer content -->
    </footer>

    <script src="js/main.js"></script>
</body>
</html>
```

### Form Standards

```html
<!-- Always include proper labels and validation -->
<form class="registration-form" method="post" action="register.php">
    <div class="form-group">
        <label for="username">Username:</label>
        <input type="text" id="username" name="username" 
               required minlength="3" maxlength="50"
               value="<?php echo htmlspecialchars($username ?? ''); ?>">
        <?php if (isset($errors['username'])): ?>
            <div class="error-message"><?php echo htmlspecialchars($errors['username']); ?></div>
        <?php endif; ?>
    </div>

    <div class="form-group">
        <label for="email">Email:</label>
        <input type="email" id="email" name="email" required
               value="<?php echo htmlspecialchars($email ?? ''); ?>">
        <?php if (isset($errors['email'])): ?>
            <div class="error-message"><?php echo htmlspecialchars($errors['email']); ?></div>
        <?php endif; ?>
    </div>

    <div class="form-group">
        <label for="password">Password:</label>
        <input type="password" id="password" name="password" 
               required minlength="8">
        <?php if (isset($errors['password'])): ?>
            <div class="error-message"><?php echo htmlspecialchars($errors['password']); ?></div>
        <?php endif; ?>
    </div>

    <button type="submit" class="btn btn-primary">Register</button>
</form>
```

---

## CSS Standards

### Class Naming (BEM-inspired)

```css
/* Use kebab-case for CSS classes */
.post-card { }                    /* Block */
.post-card__title { }            /* Element */
.post-card__content { }          /* Element */
.post-card--featured { }         /* Modifier */

/* Section 1: Simple, descriptive names */
.user-profile { }
.post-list { }
.navigation-menu { }
.error-message { }
.success-message { }

/* Section 2: More structured approach */
.component-post-card { }
.layout-sidebar { }
.utility-text-center { }
.state-is-active { }
```

### CSS Structure

```css
/* File header comment */
/**
 * Social Platform Styles - Chapter X, Lesson X.X
 * [Description of styles in this file]
 */

/* CSS Reset and Base Styles */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

/* Typography */
body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-size: 16px;
    line-height: 1.6;
    color: #333;
}

/* Layout Components */
.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
}

/* Component Styles - Group related styles together */
.post-card {
    background: #fff;
    border: 1px solid #ddd;
    border-radius: 8px;
    padding: 20px;
    margin-bottom: 20px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.post-card__header {
    display: flex;
    align-items: center;
    margin-bottom: 15px;
}

.post-card__title {
    font-size: 1.25rem;
    font-weight: 600;
    color: #2c3e50;
    margin: 0;
}

/* Utility Classes */
.text-center { text-align: center; }
.text-muted { color: #6c757d; }
.hidden { display: none; }

/* Responsive Design */
@media (max-width: 768px) {
    .container {
        padding: 0 15px;
    }

    .post-card {
        padding: 15px;
    }
}
```

---

## JavaScript Standards

### Section 1 (Learning Path) - Simple, Clear Code

```javascript
/**
 * Social Platform JavaScript - Chapter X, Lesson X.X
 * [Description of functionality]
 */

// Use clear, descriptive function names
function likePost(postId) {
    // Show loading state
    const likeButton = document.getElementById('like-button-' + postId);
    likeButton.textContent = 'Loading...';
    likeButton.disabled = true;

    // Send AJAX request
    fetch('like-post.php', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
        },
        body: JSON.stringify({ post_id: postId })
    })
    .then(response => response.json())
    .then(data => {
        if (data.success) {
            // Update button text and count
            likeButton.textContent = data.is_liked ? 'Unlike' : 'Like';
            document.getElementById('like-count-' + postId).textContent = data.like_count;
        } else {
            // Show error message
            alert('Error: ' + data.message);
        }
    })
    .catch(error => {
        console.error('Error:', error);
        alert('Something went wrong. Please try again.');
    })
    .finally(() => {
        // Re-enable button
        likeButton.disabled = false;
    });
}

// Add event listeners when page loads
document.addEventListener('DOMContentLoaded', function() {
    // Add click handlers to all like buttons
    document.querySelectorAll('.like-button').forEach(button => {
        button.addEventListener('click', function() {
            const postId = this.dataset.postId;
            likePost(postId);
        });
    });
});
```

### Section 2 (Builder's Path) - Modern JavaScript

```javascript
/**
 * Social Platform Frontend API Client
 * 
 * Handles all API communication with proper error handling
 * and loading states management.
 */

class SocialPlatformAPI {
    constructor(baseUrl) {
        this.baseUrl = baseUrl;
        this.token = localStorage.getItem('auth_token');
    }

    /**
     * Generic API request handler
     * @param {string} endpoint - API endpoint
     * @param {object} options - Fetch options
     * @returns {Promise<object>} API response
     */
    async makeRequest(endpoint, options = {}) {
        const url = `${this.baseUrl}${endpoint}`;
        const headers = {
            'Content-Type': 'application/json',
            ...options.headers
        };

        if (this.token) {
            headers.Authorization = `Bearer ${this.token}`;
        }

        try {
            const response = await fetch(url, {
                ...options,
                headers
            });

            if (!response.ok) {
                throw new Error(`HTTP ${response.status}: ${response.statusText}`);
            }

            return await response.json();
        } catch (error) {
            console.error('API Request failed:', error);
            throw error;
        }
    }

    /**
     * Toggle post like status
     * @param {number} postId - Post ID to like/unlike
     * @returns {Promise<object>} Updated like data
     */
    async togglePostLike(postId) {
        return this.makeRequest(`/posts/${postId}/like`, {
            method: 'POST'
        });
    }
}

// Initialize API client
const api = new SocialPlatformAPI('/api');

// Modern event handling with proper error management
document.addEventListener('DOMContentLoaded', () => {
    new PostInteractionHandler(api);
});
```

---

## Database Standards

### Table Naming

```sql
-- Use plural, lowercase table names with underscores
CREATE TABLE users (           -- Good
CREATE TABLE user_profiles (   -- Good
CREATE TABLE post_likes (      -- Good

CREATE TABLE User (            -- Bad (singular, capitalized)
CREATE TABLE userProfiles (    -- Bad (camelCase)
CREATE TABLE PostLikes (       -- Bad (PascalCase)
```

### Column Naming

```sql
-- Use snake_case for column names
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL UNIQUE,
    email VARCHAR(255) NOT NULL UNIQUE,
    password_hash VARCHAR(255) NOT NULL,
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    profile_picture_url VARCHAR(500),
    is_verified BOOLEAN DEFAULT FALSE,
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

-- Foreign key naming convention
CREATE TABLE posts (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,                    -- Good: table_name + _id
    category_id INT,                         -- Good
    title VARCHAR(255) NOT NULL,
    content TEXT,
    image_urls JSON,
    is_published BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,

    FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE,
    FOREIGN KEY (category_id) REFERENCES categories(id) ON DELETE SET NULL
);
```

### Query Formatting

```sql
-- Section 1: Simple, readable queries
SELECT username, email, created_at
FROM users
WHERE is_active = 1
ORDER BY created_at DESC
LIMIT 10;

-- Section 2: Complex queries with proper formatting
SELECT 
    p.id,
    p.title,
    p.content,
    p.created_at,
    u.username,
    u.profile_picture_url,
    COUNT(pl.id) as like_count,
    COUNT(c.id) as comment_count
FROM posts p
    JOIN users u ON p.user_id = u.id
    LEFT JOIN post_likes pl ON p.id = pl.post_id
    LEFT JOIN comments c ON p.id = c.post_id
WHERE p.is_published = 1
    AND u.is_active = 1
    AND p.created_at >= DATE_SUB(NOW(), INTERVAL 7 DAY)
GROUP BY p.id, u.id
ORDER BY like_count DESC, p.created_at DESC
LIMIT 20 OFFSET ?;
```

---

## Security Standards

### Input Validation and Sanitization

```php
// Always validate and sanitize user input
function validate_username($username) {
    // Remove whitespace
    $username = trim($username);

    // Check length
    if (strlen($username) < 3 || strlen($username) > 50) {
        return false;
    }

    // Check characters (alphanumeric and underscores only)
    if (!preg_match('/^[a-zA-Z0-9_]+$/', $username)) {
        return false;
    }

    return true;
}

function sanitize_input($input) {
    return htmlspecialchars(trim($input), ENT_QUOTES, 'UTF-8');
}

// Example usage
if ($_POST['username']) {
    $username = $_POST['username'];

    if (!validate_username($username)) {
        $errors['username'] = 'Username must be 3-50 characters, letters, numbers, and underscores only.';
    } else {
        $clean_username = sanitize_input($username);
        // Proceed with clean data
    }
}
```

### Database Security

```php
// Always use prepared statements
// NEVER concatenate user input directly into SQL

// Good - Prepared statement
$stmt = $pdo->prepare("SELECT * FROM users WHERE username = ? AND email = ?");
$stmt->execute([$username, $email]);

// Bad - Direct concatenation (SQL injection vulnerable)
$sql = "SELECT * FROM users WHERE username = '$username' AND email = '$email'";
$result = $pdo->query($sql);

// For dynamic WHERE clauses, build safely
$conditions = [];
$params = [];

if ($username) {
    $conditions[] = "username = ?";
    $params[] = $username;
}

if ($email) {
    $conditions[] = "email = ?";
    $params[] = $email;
}

if ($conditions) {
    $sql = "SELECT * FROM users WHERE " . implode(" AND ", $conditions);
    $stmt = $pdo->prepare($sql);
    $stmt->execute($params);
}
```

---

## Error Handling Standards

### Section 1 (Learning Path) - Simple Error Handling

```php
// Basic error handling with user-friendly messages
try {
    $pdo = new PDO($dsn, $username, $password);
    $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
} catch (PDOException $e) {
    // Log the real error for developers
    error_log("Database connection failed: " . $e->getMessage());

    // Show generic message to users
    die("Sorry, we're having technical difficulties. Please try again later.");
}

// Form processing with error collection
$errors = [];

if ($_POST['submit']) {
    // Validate each field
    if (empty($_POST['username'])) {
        $errors['username'] = 'Username is required.';
    } elseif (!validate_username($_POST['username'])) {
        $errors['username'] = 'Username must be 3-50 characters, letters and numbers only.';
    }

    if (empty($_POST['email'])) {
        $errors['email'] = 'Email is required.';
    } elseif (!filter_var($_POST['email'], FILTER_VALIDATE_EMAIL)) {
        $errors['email'] = 'Please enter a valid email address.';
    }

    // If no errors, proceed
    if (empty($errors)) {
        // Process the form
        try {
            // Database operations
        } catch (PDOException $e) {
            error_log("Registration failed: " . $e->getMessage());
            $errors['general'] = 'Registration failed. Please try again.';
        }
    }
}
```

### Section 2 (Builder's Path) - Professional Error Handling

```php
// Custom exception classes
class ValidationException extends Exception
{
    private array $errors;

    public function __construct(array $errors, string $message = "Validation failed")
    {
        $this->errors = $errors;
        parent::__construct($message);
    }

    public function getErrors(): array
    {
        return $this->errors;
    }
}

class DatabaseException extends Exception { }

// Service class with proper error handling
class UserService
{
    private PDO $db;
    private LoggerInterface $logger;

    public function createUser(array $userData): User
    {
        // Validate input
        $errors = $this->validateUserData($userData);
        if (!empty($errors)) {
            throw new ValidationException($errors);
        }

        try {
            $this->db->beginTransaction();

            // Create user record
            $stmt = $this->db->prepare(
                "INSERT INTO users (username, email, password_hash) VALUES (?, ?, ?)"
            );
            $stmt->execute([
                $userData['username'],
                $userData['email'],
                password_hash($userData['password'], PASSWORD_DEFAULT)
            ]);

            $userId = $this->db->lastInsertId();

            // Create profile record
            $stmt = $this->db->prepare(
                "INSERT INTO user_profiles (user_id, first_name, last_name) VALUES (?, ?, ?)"
            );
            $stmt->execute([
                $userId,
                $userData['first_name'] ?? '',
                $userData['last_name'] ?? ''
            ]);

            $this->db->commit();

            $this->logger->info("User created successfully", ['user_id' => $userId]);

            return $this->findById($userId);

        } catch (PDOException $e) {
            $this->db->rollBack();
            $this->logger->error("User creation failed", [
                'error' => $e->getMessage(),
                'user_data' => array_diff_key($userData, ['password' => ''])
            ]);
            throw new DatabaseException("Failed to create user account");
        }
    }
}
```

---

## Testing Standards

### Section 2 - Unit Testing with PHPUnit

```php
<?php
/**
 * User Service Test Suite
 */

use PHPUnit\Framework\TestCase;
use SocialPlatform\Services\UserService;
use SocialPlatform\Exceptions\ValidationException;

class UserServiceTest extends TestCase
{
    private UserService $userService;
    private PDO $testDb;

    protected function setUp(): void
    {
        // Set up test database
        $this->testDb = new PDO('sqlite::memory:');
        $this->createTestTables();

        // Initialize service with test dependencies
        $this->userService = new UserService($this->testDb, new TestLogger());
    }

    public function testCreateUserWithValidData(): void
    {
        $userData = [
            'username' => 'testuser',
            'email' => 'test@example.com',
            'password' => 'securepassword123',
            'first_name' => 'Test',
            'last_name' => 'User'
        ];

        $user = $this->userService->createUser($userData);

        $this->assertNotNull($user->getId());
        $this->assertEquals('testuser', $user->getUsername());
        $this->assertEquals('test@example.com', $user->getEmail());
    }

    public function testCreateUserWithInvalidDataThrowsValidationException(): void
    {
        $this->expectException(ValidationException::class);

        $userData = [
            'username' => 'ab', // Too short
            'email' => 'invalid-email',
            'password' => '123' // Too short
        ];

        $this->userService->createUser($userData);
    }

    private function createTestTables(): void
    {
        $this->testDb->exec("
            CREATE TABLE users (
                id INTEGER PRIMARY KEY AUTOINCREMENT,
                username VARCHAR(50) NOT NULL UNIQUE,
                email VARCHAR(255) NOT NULL UNIQUE,
                password_hash VARCHAR(255) NOT NULL,
                created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
            )
        ");

        $this->testDb->exec("
            CREATE TABLE user_profiles (
                id INTEGER PRIMARY KEY AUTOINCREMENT,
                user_id INTEGER NOT NULL,
                first_name VARCHAR(100),
                last_name VARCHAR(100),
                FOREIGN KEY (user_id) REFERENCES users(id)
            )
        ");
    }
}
?>
```

---

## Documentation Standards

### Inline Documentation

```php
/**
 * Processes user registration form submission
 * 
 * This function validates user input, checks for existing accounts,
 * creates a new user record, and sends a welcome email.
 * 
 * @param array $form_data POST data from registration form
 * @return array Contains 'success' boolean and 'message' string
 * @throws DatabaseException When database operations fail
 * @throws EmailException When welcome email cannot be sent
 * 
 * @example
 * $result = process_registration($_POST);
 * if ($result['success']) {
 *     redirect('welcome.php');
 * } else {
 *     show_error($result['message']);
 * }
 */
function process_registration($form_data) {
    // Implementation
}
```

### README Files

```markdown
# Social Platform - Chapter X

## What This Chapter Covers

Brief description of what students will learn and build.

## Files Created/Modified

- `filename.php` - Description of purpose
- `style.css` - Styling for new features
- `database.sql` - New table structures

## Prerequisites

- Completed Chapter X-1
- Understanding of [specific concepts]

## Testing Your Code

1. Navigate to `http://localhost/your-project/`
2. Test specific functionality
3. Verify expected results

## Common Issues

### Problem: Error message or symptom
**Solution:** Step-by-step fix

### Problem: Another common issue
**Solution:** How to resolve it

## Next Steps

Preview of what comes next in Chapter X+1.
```

This comprehensive code style guide ensures consistency, readability, and maintainability across all 120+ lessons while teaching professional development practices!
