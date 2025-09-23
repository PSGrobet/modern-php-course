# Chapter 1, Lesson 1.5: Input Validation & Security Basics

**Goal:** Implement comprehensive input validation and security practices to protect your platform from attacks  
**Time:** 1-2 hours  
**Prerequisites:** Lessons 1.1-1.4 - PHP basics through form processing  
**New Code:** ~290 lines PHP + HTML

---

## What You'll Build

In this lesson, you will:

- Create a validation library with reusable security functions
- Build a secure login form with proper authentication checks
- Implement CSRF protection for forms
- Learn about common web vulnerabilities and how to prevent them
- Create a user session management system

---

## Why This Matters

Security isn't optional in web development - it's essential from day one. Every form, every user input, every data display is a potential attack vector. Understanding validation and security principles protects both your platform and your users.

Real social platforms face constant attacks: SQL injection, XSS, CSRF, session hijacking, and more. The security practices you learn here are used by every professional PHP application.

---

## Core Concept: Defense in Depth

**Definition:** Security through multiple layers - validate input, escape output, protect sessions, verify permissions, and log suspicious activity.

**Key Principles:**

- Never trust user input
- Validate everything server-side
- Use prepared statements for databases
- Escape all output
- Protect against common attacks

**In Our Platform:** Every form, login, and user action will be secured using these principles.

---

## Step-by-Step Implementation

### Step 1: Create Security Validation Library

**What we're doing:** Building reusable validation functions for common security checks

Create a file called `security.php`:

```php
<?php
/**
 * Social Platform - Chapter 1, Lesson 1.5
 * Security Functions - Input validation and protection
 */

/**
 * Validate username format and security
 */
function validate_username($username) {
    $username = trim($username);

    if (empty($username)) {
        return 'Username is required';
    }

    if (strlen($username) < 3 || strlen($username) > 30) {
        return 'Username must be 3-30 characters';
    }

    if (!preg_match('/^[a-zA-Z0-9_]+$/', $username)) {
        return 'Username can only contain letters, numbers, and underscores';
    }

    $blocked_usernames = ['admin', 'administrator', 'root', 'system', 'test'];
    if (in_array(strtolower($username), $blocked_usernames)) {
        return 'This username is not available';
    }

    return true;
}

/**
 * Validate email with security checks
 */
function validate_email($email) {
    $email = trim($email);

    if (empty($email)) {
        return 'Email is required';
    }

    if (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
        return 'Please enter a valid email address';
    }

    if (strlen($email) > 255) {
        return 'Email address is too long';
    }

    return true;
}

/**
 * Validate password strength
 */
function validate_password($password) {
    if (empty($password)) {
        return 'Password is required';
    }

    if (strlen($password) < 8) {
        return 'Password must be at least 8 characters';
    }

    if (strlen($password) > 128) {
        return 'Password is too long (max 128 characters)';
    }

    if (!preg_match('/[A-Z]/', $password)) {
        return 'Password must contain at least one uppercase letter';
    }

    if (!preg_match('/[a-z]/', $password)) {
        return 'Password must contain at least one lowercase letter';
    }

    if (!preg_match('/[0-9]/', $password)) {
        return 'Password must contain at least one number';
    }

    return true;
}

/**
 * Sanitize text input for safe storage
 */
function sanitize_text($text, $max_length = 1000) {
    $text = trim($text);
    $text = strip_tags($text);

    if (strlen($text) > $max_length) {
        $text = substr($text, 0, $max_length);
    }

    return $text;
}

/**
 * Generate CSRF token for form protection
 */
function generate_csrf_token() {
    if (session_status() === PHP_SESSION_NONE) {
        session_start();
    }

    if (!isset($_SESSION['csrf_token'])) {
        $_SESSION['csrf_token'] = bin2hex(random_bytes(32));
    }

    return $_SESSION['csrf_token'];
}

/**
 * Validate CSRF token
 */
function validate_csrf_token($token) {
    if (session_status() === PHP_SESSION_NONE) {
        session_start();
    }

    return isset($_SESSION['csrf_token']) && 
           hash_equals($_SESSION['csrf_token'], $token);
}

/**
 * Rate limiting - simple session-based approach
 */
function check_rate_limit($action, $max_attempts = 5, $time_window = 300) {
    if (session_status() === PHP_SESSION_NONE) {
        session_start();
    }

    $key = "rate_limit_{$action}";
    $now = time();

    if (!isset($_SESSION[$key])) {
        $_SESSION[$key] = [];
    }

    $_SESSION[$key] = array_filter($_SESSION[$key], function($timestamp) use ($now, $time_window) {
        return ($now - $timestamp) < $time_window;
    });

    if (count($_SESSION[$key]) >= $max_attempts) {
        return false;
    }

    $_SESSION[$key][] = $now;
    return true;
}

/**
 * Log security events
 */
function log_security_event($event, $details = []) {
    $log_entry = [
        'timestamp' => date('Y-m-d H:i:s'),
        'ip' => $_SERVER['REMOTE_ADDR'] ?? 'unknown',
        'user_agent' => $_SERVER['HTTP_USER_AGENT'] ?? 'unknown',
        'event' => $event,
        'details' => $details
    ];

    error_log("SECURITY: " . json_encode($log_entry));
}
?>
```

### Step 2: Create Secure Login Form

**What we're doing:** Building a login form that demonstrates proper security practices

Create a file called `login.php`:

```php
<?php
/**
 * Social Platform - Chapter 1, Lesson 1.5
 * Secure Login - Demonstrates authentication security
 */

require_once 'functions.php';
require_once 'security.php';

$page_title = 'Login - Social Platform';

session_start();

$errors = [];
$form_data = ['username' => ''];

if ($_POST) {
    if (!validate_csrf_token($_POST['csrf_token'] ?? '')) {
        log_security_event('csrf_violation', ['action' => 'login']);
        $errors['general'] = 'Security error. Please refresh and try again.';
    } elseif (!check_rate_limit('login_attempts', 5, 300)) {
        log_security_event('rate_limit_exceeded', ['action' => 'login']);
        $errors['general'] = 'Too many login attempts. Please wait 5 minutes.';
    } else {
        $username = sanitize_text($_POST['username'] ?? '', 30);
        $password = $_POST['password'] ?? '';

        $form_data['username'] = $username;

        $username_validation = validate_username($username);
        if ($username_validation !== true) {
            $errors['username'] = $username_validation;
        }

        if (empty($password)) {
            $errors['password'] = 'Password is required';
        }

        if (empty($errors)) {
            $demo_users = [
                'demo_user' => password_hash('password123', PASSWORD_DEFAULT),
                'sarah_dev' => password_hash('SecurePass1', PASSWORD_DEFAULT),
                'test_user' => password_hash('TestPass1', PASSWORD_DEFAULT)
            ];

            if (isset($demo_users[$username]) && 
                password_verify($password, $demo_users[$username])) {

                $_SESSION['user_id'] = array_search($username, array_keys($demo_users)) + 1;
                $_SESSION['username'] = $username;
                $_SESSION['login_time'] = time();

                session_regenerate_id(true);

                log_security_event('successful_login', ['username' => $username]);

                header('Location: dashboard.php');
                exit;
            } else {
                log_security_event('failed_login', ['username' => $username]);
                $errors['general'] = 'Invalid username or password';
            }
        }
    }
}

include 'header.php';
?>

        <div class="card" style="max-width: 400px; margin: 50px auto;">
            <h1 class="title text-center">Welcome Back</h1>
            <p class="text text-center">Sign in to your account</p>

            <?php if (isset($errors['general'])): ?>
                <div class="form-error" style="text-align: center; margin-bottom: 20px;">
                    <strong><?php echo htmlspecialchars($errors['general']); ?></strong>
                </div>
            <?php endif; ?>

            <form method="post" action="login.php">
                <input type="hidden" name="csrf_token" value="<?php echo generate_csrf_token(); ?>">

                <div class="form-group">
                    <label class="label" for="username">Username</label>
                    <input type="text" 
                           id="username" 
                           name="username" 
                           class="input" 
                           value="<?php echo htmlspecialchars($form_data['username']); ?>"
                           required 
                           autocomplete="username">
                    <?php if (isset($errors['username'])): ?>
                        <div class="form-error"><?php echo htmlspecialchars($errors['username']); ?></div>
                    <?php endif; ?>
                </div>

                <div class="form-group">
                    <label class="label" for="password">Password</label>
                    <input type="password" 
                           id="password" 
                           name="password" 
                           class="input" 
                           required 
                           autocomplete="current-password">
                    <?php if (isset($errors['password'])): ?>
                        <div class="form-error"><?php echo htmlspecialchars($errors['password']); ?></div>
                    <?php endif; ?>
                </div>

                <button type="submit" class="btn btn-primary" style="width: 100%; margin-top: 10px;">
                    Sign In
                </button>
            </form>

            <div class="text-center" style="margin-top: 30px;">
                <p class="muted">Demo accounts:</p>
                <p class="muted" style="font-size: 0.8rem;">
                    demo_user / password123<br>
                    sarah_dev / SecurePass1<br>
                    test_user / TestPass1
                </p>
            </div>

            <div class="text-center" style="margin-top: 20px;">
                <p class="muted">Don't have an account? <a href="register.php" style="color: #007acc;">Register here</a></p>
            </div>
        </div>

    </main>
</body>
</html>
```

---

## Testing Your Work

### Security Testing:

1. **Test the login form** with demo credentials
2. **Try invalid passwords** - should show generic error message
3. **Test rate limiting** - make 6 failed attempts quickly
4. **Check CSRF protection** - try submitting form without token (manually remove hidden field)
5. **Test validation** - try usernames with special characters

### Quick Verification:

1. Save both files: `security.php` and `login.php`
2. Open `http://localhost/login.php`
3. Try logging in with `demo_user` / `password123`
4. Test various security scenarios above

### Troubleshooting:

**Issue:** Session errors  
**Fix:** Make sure your server supports sessions and has write permissions

**Issue:** Rate limiting not working  
**Fix:** Sessions must be working properly for rate limiting

**Issue:** CSRF token errors  
**Fix:** Ensure sessions are started before generating tokens

---

## What You've Accomplished

✅ **Built a security validation library** with reusable functions  
✅ **Implemented proper password hashing** and verification  
✅ **Added CSRF protection** to prevent cross-site attacks  
✅ **Created rate limiting** to prevent brute force attacks  
✅ **Added security logging** to track suspicious activity  
✅ **Built secure authentication** with session management

**Your platform now has:** Professional-grade security measures that protect against common web vulnerabilities.

---

## Next Up

**Chapter 2, Lesson 2.1:** Database Design - Users, Posts, and Relationships

We'll design and create the MySQL database structure that will replace our arrays with persistent, scalable data storage.

---

## 💡 Security Learning Notes

- **Defense in depth:** Multiple security layers protect better than one
- **Rate limiting:** Prevents automated attacks and abuse
- **CSRF tokens:** Protect against cross-site request forgery
- **Password hashing:** Never store plain text passwords
- **Session security:** Regenerate IDs after login, validate sessions
- **Input validation:** Server-side validation is mandatory, client-side is convenience

These security principles apply to every web application, not just social platforms! 
