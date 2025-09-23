# Chapter 1, Lesson 1.4: Forms & User Input - Registration and Content Creation

**Goal:** Handle user input through HTML forms and PHP processing for registration and post creation  
**Time:** 1-2 hours  
**Prerequisites:** Lessons 1.1-1.3 - PHP basics, arrays, and functions  
**New Code:** ~95 lines PHP/HTML

---

## What You'll Build

In this lesson, you will:

- Create HTML forms for user registration and post creation
- Process form data using PHP's `$_POST` superglobal
- Implement basic form validation and error handling
- Build a user registration system that stores data temporarily
- Create a post creation form that adds to your platform feed

---

## Why This Matters

Forms are how users interact with social platforms - registering accounts, creating posts, commenting, updating profiles. Understanding form processing is essential because every user action requires securely handling input data.

PHP's form handling connects frontend HTML to backend processing. This is where security becomes critical - all user input must be validated and sanitized to prevent attacks and ensure data integrity.

---

## Core Concept: Form Processing with PHP

**Definition:** HTML forms send data to PHP scripts using GET or POST methods. PHP receives this data through superglobal arrays like `$_POST` and `$_GET`.

**Syntax:**

```php
<!-- HTML Form -->
<form method="post" action="process.php">
    <input type="text" name="username" required>
    <button type="submit">Submit</button>
</form>

<?php
// PHP Processing
if ($_POST) {
    $username = $_POST['username'];
    // Validate and process the data
}
?>
```

**In Our Platform:** Forms will handle user registration, login, post creation, comments, and all user-generated content that makes the platform interactive.

---

## Step-by-Step Implementation

### Step 1: Add Form Styles to CSS

**What we're doing:** Adding form-specific styles to our existing styles.css

Add these styles to your existing `styles.css` file:

```css
/* Form Components - Add to existing styles.css */
.form-group {
    margin-bottom: 15px;
}

.label {
    display: block;
    color: #ccc;
    margin-bottom: 5px;
    font-weight: bold;
}

.input {
    width: 100%;
    padding: 12px;
    background: #333;
    color: #fff;
    border: 1px solid #555;
    border-radius: 3px;
    box-sizing: border-box;
    font-size: 14px;
}

.input:focus {
    border-color: #007acc;
    outline: none;
}

.textarea {
    width: 100%;
    padding: 12px;
    background: #333;
    color: #fff;
    border: 1px solid #555;
    border-radius: 3px;
    box-sizing: border-box;
    font-size: 14px;
    min-height: 100px;
    resize: vertical;
}

.textarea:focus {
    border-color: #007acc;
    outline: none;
}

.form-error {
    color: #ff6b6b;
    font-size: 0.9rem;
    margin-top: 5px;
}

.form-success {
    color: #51cf66;
    font-size: 0.9rem;
    margin-top: 5px;
}
```

### Step 2: Create Registration Form

**What we're doing:** Building a user registration form with validation

Create a file called `register.php`:

```php
<?php
/**
 * Social Platform - Chapter 1, Lesson 1.4
 * User Registration - Form processing and validation
 */

require_once 'functions.php';
$page_title = 'Register - Social Platform';

// Initialize variables
$errors = [];
$success = false;
$form_data = [
    'username' => '',
    'email' => '',
    'full_name' => '',
    'bio' => ''
];

// Process form submission
if ($_POST) {
    // Get form data and trim whitespace
    $form_data['username'] = trim($_POST['username'] ?? '');
    $form_data['email'] = trim($_POST['email'] ?? '');
    $form_data['full_name'] = trim($_POST['full_name'] ?? '');
    $form_data['bio'] = trim($_POST['bio'] ?? '');
    $password = $_POST['password'] ?? '';
    $confirm_password = $_POST['confirm_password'] ?? '';

    // Validation
    if (empty($form_data['username'])) {
        $errors['username'] = 'Username is required';
    } elseif (strlen($form_data['username']) < 3) {
        $errors['username'] = 'Username must be at least 3 characters';
    } elseif (!preg_match('/^[a-zA-Z0-9_]+$/', $form_data['username'])) {
        $errors['username'] = 'Username can only contain letters, numbers, and underscores';
    }

    if (empty($form_data['email'])) {
        $errors['email'] = 'Email is required';
    } elseif (!filter_var($form_data['email'], FILTER_VALIDATE_EMAIL)) {
        $errors['email'] = 'Please enter a valid email address';
    }

    if (empty($form_data['full_name'])) {
        $errors['full_name'] = 'Full name is required';
    }

    if (empty($password)) {
        $errors['password'] = 'Password is required';
    } elseif (strlen($password) < 6) {
        $errors['password'] = 'Password must be at least 6 characters';
    }

    if ($password !== $confirm_password) {
        $errors['confirm_password'] = 'Passwords do not match';
    }

    // If no errors, "register" the user (in real app, save to database)
    if (empty($errors)) {
        $success = true;
        // Clear form data on success
        $form_data = ['username' => '', 'email' => '', 'full_name' => '', 'bio' => ''];
    }
}

include 'header.php';
?>

        <div class="card">
            <h1 class="title">Create Your Account</h1>
            <p class="text">Join our social platform and connect with developers worldwide</p>

            <?php if ($success): ?>
                <div class="form-success">
                    <strong>Registration successful!</strong> Welcome to the platform, <?php echo htmlspecialchars($_POST['full_name']); ?>!
                </div>
            <?php endif; ?>

            <form method="post" action="register.php">
                <div class="form-group">
                    <label class="label" for="username">Username</label>
                    <input type="text" 
                           id="username" 
                           name="username" 
                           class="input" 
                           value="<?php echo htmlspecialchars($form_data['username']); ?>"
                           placeholder="e.g. john_doe">
                    <?php if (isset($errors['username'])): ?>
                        <div class="form-error"><?php echo $errors['username']; ?></div>
                    <?php endif; ?>
                </div>

                <div class="form-group">
                    <label class="label" for="email">Email Address</label>
                    <input type="email" 
                           id="email" 
                           name="email" 
                           class="input" 
                           value="<?php echo htmlspecialchars($form_data['email']); ?>"
                           placeholder="your@email.com">
                    <?php if (isset($errors['email'])): ?>
                        <div class="form-error"><?php echo $errors['email']; ?></div>
                    <?php endif; ?>
                </div>

                <div class="form-group">
                    <label class="label" for="full_name">Full Name</label>
                    <input type="text" 
                           id="full_name" 
                           name="full_name" 
                           class="input" 
                           value="<?php echo htmlspecialchars($form_data['full_name']); ?>"
                           placeholder="John Smith">
                    <?php if (isset($errors['full_name'])): ?>
                        <div class="form-error"><?php echo $errors['full_name']; ?></div>
                    <?php endif; ?>
                </div>

                <div class="form-group">
                    <label class="label" for="bio">Bio (Optional)</label>
                    <textarea id="bio" 
                              name="bio" 
                              class="textarea" 
                              placeholder="Tell us about yourself..."><?php echo htmlspecialchars($form_data['bio']); ?></textarea>
                </div>

                <div class="form-group">
                    <label class="label" for="password">Password</label>
                    <input type="password" 
                           id="password" 
                           name="password" 
                           class="input" 
                           placeholder="At least 6 characters">
                    <?php if (isset($errors['password'])): ?>
                        <div class="form-error"><?php echo $errors['password']; ?></div>
                    <?php endif; ?>
                </div>

                <div class="form-group">
                    <label class="label" for="confirm_password">Confirm Password</label>
                    <input type="password" 
                           id="confirm_password" 
                           name="confirm_password" 
                           class="input" 
                           placeholder="Re-enter your password">
                    <?php if (isset($errors['confirm_password'])): ?>
                        <div class="form-error"><?php echo $errors['confirm_password']; ?></div>
                    <?php endif; ?>
                </div>

                <button type="submit" class="btn btn-primary" style="width: 100%;">
                    Create Account
                </button>
            </form>

            <div class="text-center" style="margin-top: 20px;">
                <p class="muted">Already have an account? <a href="#" style="color: #007acc;">Sign in here</a></p>
            </div>
        </div>

        <!-- Display submitted data for learning purposes -->
        <?php if ($_POST && !empty($errors)): ?>
            <div class="card">
                <h2 class="title">Debug: Form Data Received</h2>
                <pre class="text" style="background: #1a1a1a; padding: 10px; border-radius: 3px;">
<?php print_r(array_map('htmlspecialchars', $_POST)); ?>
                </pre>
            </div>
        <?php endif; ?>

    </main>
</body>
</html>
```

### Step 3: Create Post Creation Form

**What we're doing:** Building a form to create new posts and add them to the platform

Create a file called `create-post.php`:

```php
<?php
/**
 * Social Platform - Chapter 1, Lesson 1.4
 * Create Post - Form for adding new posts
 */

require_once 'functions.php';
$page_title = 'Create Post - Social Platform';

// Initialize variables
$errors = [];
$success = false;
$post_content = '';

// Process form submission
if ($_POST) {
    $post_content = trim($_POST['content'] ?? '');

    // Validation
    if (empty($post_content)) {
        $errors['content'] = 'Post content is required';
    } elseif (strlen($post_content) < 10) {
        $errors['content'] = 'Post must be at least 10 characters long';
    } elseif (strlen($post_content) > 500) {
        $errors['content'] = 'Post cannot exceed 500 characters';
    }

    // If no errors, "create" the post
    if (empty($errors)) {
        $success = true;
        $post_content = ''; // Clear form on success
    }
}

include 'header.php';
?>

        <div class="card">
            <h1 class="title">Create New Post</h1>
            <p class="text">Share your thoughts with the community</p>

            <?php if ($success): ?>
                <div class="form-success">
                    <strong>Post created successfully!</strong> Your post has been added to your feed.
                </div>
            <?php endif; ?>

            <form method="post" action="create-post.php">
                <div class="form-group">
                    <label class="label" for="content">What's on your mind?</label>
                    <textarea id="content" 
                              name="content" 
                              class="textarea" 
                              style="min-height: 120px;"
                              placeholder="Share your thoughts, ask a question, or start a discussion..."><?php echo htmlspecialchars($post_content); ?></textarea>

                    <div style="margin-top: 5px;" class="flex">
                        <span class="muted">
                            Characters: <span id="char-count">0</span>/500
                        </span>
                        <div style="margin-left: auto;">
                            <?php if (isset($errors['content'])): ?>
                                <span class="form-error"><?php echo $errors['content']; ?></span>
                            <?php endif; ?>
                        </div>
                    </div>
                </div>

                <div class="form-group">
                    <button type="submit" class="btn btn-primary">
                        📝 Publish Post
                    </button>
                    <a href="dashboard.php" class="btn" style="margin-left: 10px;">Cancel</a>
                </div>
            </form>
        </div>

        <!-- Recent posts preview -->
        <div class="card">
            <h2 class="title">Your Recent Posts</h2>
            <p class="muted">Posts you've created will appear here</p>

            <?php if ($success && $_POST): ?>
                <!-- Show the "new" post -->
                <div class="card" style="background: #1a4a1a; border: 1px solid #4a7c4a;">
                    <div class="flex">
                        <div class="user-avatar">
                            <?php echo get_user_initials('Your Name'); ?>
                        </div>
                        <div class="user-info">
                            <h4 style="margin: 0; color: #fff;">Your Name</h4>
                            <p class="muted" style="margin: 0;">@your_username • just now</p>
                        </div>
                    </div>
                    <div class="text" style="margin-top: 15px;">
                        <?php echo nl2br(htmlspecialchars($_POST['content'])); ?>
                    </div>
                    <div class="muted" style="margin-top: 10px;">

                    </div>
                </div>
            <?php endif; ?>

            <div class="text-center">
                <p class="muted">No posts yet. Create your first post above!</p>
            </div>
        </div>

    <script>
        // Character counter for textarea
        const textarea = document.getElementById('content');
        const charCount = document.getElementById('char-count');

        if (textarea && charCount) {
            // Update count on page load
            charCount.textContent = textarea.value.length;

            // Update count as user types
            textarea.addEventListener('input', function() {
                charCount.textContent = this.value.length;

                // Change color based on length
                if (this.value.length > 450) {
                    charCount.style.color = '#ff6b6b';
                } else if (this.value.length > 400) {
                    charCount.style.color = '#ffd43b';
                } else {
                    charCount.style.color = '#888';
                }
            });
        }
    </script>

    </main>
</body>
</html>
```

---

## Testing Your Work

### Quick Verification:

1. Save both new files: `register.php` and `create-post.php`
2. Add the new CSS styles to your existing `styles.css`
3. Test the registration form at `http://localhost/register.php`
4. Try submitting with invalid data to see validation errors
5. Test the post creation form at `http://localhost/create-post.php`
6. Verify the character counter works as you type

### Troubleshooting:

**Issue:** Form doesn't submit or shows blank page  
**Fix:** Check that your form action and method attributes are correct

**Issue:** Validation errors not showing  
**Fix:** Ensure error array keys match your input names exactly

**Issue:** Character counter not working  
**Fix:** Verify that the JavaScript IDs match your HTML element IDs

---

## What You've Accomplished

✅ **Built HTML forms** for user registration and content creation  
✅ **Processed form data** using PHP's `$_POST` superglobal  
✅ **Implemented validation** with error handling and user feedback  
✅ **Added form styles** that match the platform's dark theme  
✅ **Created interactive features** like character counters with JavaScript

**Your platform can now:** Accept and validate user input, provide helpful error messages, and create new content through forms.

---

## Next Up

**Lesson 1.5:** Input Validation & Security Basics

We'll learn advanced validation techniques and security practices to protect your platform from common attacks and ensure data integrity.

---

## 💡 PHP Learning Notes

- **Always validate input:** Never trust user data - validate everything server-side
- **Preserve form data:** Keep user input in forms when showing validation errors
- **Use htmlspecialchars():** Prevent XSS attacks by escaping user output
- **POST vs GET:** Use POST for forms that change data, GET for search/filtering
- **Superglobals:** `$_POST`, `$_GET`, and `$_SESSION` are available everywhere in PHP

This lesson establishes the foundation for all user interactions in your platform!
