# Chapter 1, Lesson 1.1: PHP Syntax & Variables - User Data Handling

**Goal:** Learn PHP syntax and variables by creating your first dynamic social platform page that displays user information  
**Time:** 1-2 hours  
**Prerequisites:** Basic HTML/CSS knowledge, understanding of programming variables  
**New Code:** ~80 lines PHP/HTML

---

## What You'll Build

In this lesson, you will:

- Create your first PHP file that combines HTML and PHP code
- Use PHP variables to store and display user information
- Learn PHP syntax including tags, comments, and basic output
- Build a simple user profile page that displays dynamic content

---

## Why This Matters

PHP is a server-side language that runs before HTML reaches the browser. This means you can generate different HTML content based on data, user actions, or database information. Understanding PHP variables and syntax is fundamental to building any dynamic web application.

In social platforms, user data changes constantly - new posts, profile updates, different users viewing pages. PHP variables let us store and manipulate this changing information before sending customized HTML to each user's browser.

---

## Core Concept: PHP Variables and Output

**Definition:** PHP variables store data that can change during script execution. They always start with a dollar sign ($) and can hold text, numbers, or complex data structures.

**Syntax:**

```php
<?php
$username = "john_doe";           // String variable
$post_count = 42;                // Integer variable
$is_verified = true;             // Boolean variable

// Output variables to HTML
echo $username;                  // Displays: john_doe
echo "Posts: " . $post_count;   // Displays: Posts: 42
?>
```

**In Our Platform:** Variables will store user information like usernames, post counts, profile data, and login status that changes for each user.

---

## Step-by-Step Implementation

### Step 1: Create the Shared CSS File

**What we're doing:** Setting up the dark theme styles that all lessons in this chapter will share

Create a file called `styles.css`:

```css
/* Chapter 1 styles.css - Shared across all lessons */

/* Base Theme */
body {
    background: #1a1a1a;
    color: #ccc;
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    line-height: 1.6;
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
    border: 1px solid #333;
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
    margin-top: 0;
}

.text {
    color: #ccc;
    line-height: 1.5;
    margin-bottom: 10px;
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
    font-size: 14px;
}

.btn-primary {
    background: #007acc;
}

.btn:hover {
    opacity: 0.9;
}

/* Platform Components */
.user-profile {
    background: #2a2a2a;
    padding: 20px;
    border-radius: 5px;
    margin: 15px 0;
}

.user-avatar {
    width: 60px;
    height: 60px;
    border-radius: 50%;
    background: #444;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 24px;
    color: #fff;
}

.user-info {
    flex: 1;
    margin-left: 15px;
}

.user-stats {
    display: flex;
    gap: 20px;
    margin-top: 15px;
}

.stat {
    text-align: center;
}

.stat-number {
    font-size: 1.2rem;
    font-weight: bold;
    color: #fff;
}

.stat-label {
    font-size: 0.9rem;
    color: #888;
}

/* Navigation */
.nav {
    background: #333;
    padding: 15px 0;
    margin-bottom: 20px;
}

.nav-link {
    color: #ccc;
    text-decoration: none;
    padding: 10px 15px;
    display: inline-block;
    border-radius: 3px;
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

### Step 2: Create Your First PHP Page

**What we're doing:** Building a user profile page that demonstrates PHP variables and basic syntax

Create a file called `user-profile.php`:

```php
<?php
/**
 * Social Platform - Chapter 1, Lesson 1.1
 * User Profile Page - Demonstrates PHP variables and basic syntax
 */

// PHP variables storing user information
// In real applications, this data would come from a database
$username = "sarah_dev";
$full_name = "Sarah Johnson";
$bio = "Full-stack developer who loves building social platforms with PHP!";
$post_count = 127;
$follower_count = 2456;
$following_count = 189;
$join_date = "March 2024";
$is_verified = true;
$location = "San Francisco, CA";

// Calculate some dynamic values
$total_interactions = $post_count + $follower_count;
$account_age_months = 8; // Could be calculated from join_date

// Create user's initials for avatar
$initials = substr($full_name, 0, 1) . substr(strstr($full_name, ' '), 1, 1);
?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title><?php echo $full_name; ?> - Social Platform</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <nav class="nav">
        <div class="container">
            <a href="#" class="nav-link">Home</a>
            <a href="#" class="nav-link">Profile</a>
            <a href="#" class="nav-link">Messages</a>
            <a href="#" class="nav-link">Settings</a>
        </div>
    </nav>

    <main class="container">
        <div class="card">
            <h1 class="title">User Profile</h1>

            <div class="user-profile">
                <div class="flex">
                    <div class="user-avatar">
                        <?php echo $initials; ?>
                    </div>
                    <div class="user-info">
                        <h2 class="title">
                            <?php echo $full_name; ?>
                            <?php if ($is_verified): ?>
                                <span style="color: #007acc;">✓</span>
                            <?php endif; ?>
                        </h2>
                        <p class="muted">@<?php echo $username; ?></p>
                        <p class="text"><?php echo $bio; ?></p>
                        <p class="muted">📍 <?php echo $location; ?> • Joined <?php echo $join_date; ?></p>
                    </div>
                </div>

                <div class="user-stats">
                    <div class="stat">
                        <div class="stat-number"><?php echo $post_count; ?></div>
                        <div class="stat-label">Posts</div>
                    </div>
                    <div class="stat">
                        <div class="stat-number"><?php echo number_format($follower_count); ?></div>
                        <div class="stat-label">Followers</div>
                    </div>
                    <div class="stat">
                        <div class="stat-number"><?php echo $following_count; ?></div>
                        <div class="stat-label">Following</div>
                    </div>
                </div>

                <div class="text-center" style="margin-top: 20px;">
                    <a href="#" class="btn btn-primary">Follow</a>
                    <a href="#" class="btn">Message</a>
                </div>
            </div>

            <!-- Additional info card -->
            <div class="card">
                <h3 class="title">Account Statistics</h3>
                <div class="text">
                    <p><strong>Account Activity:</strong> <?php echo number_format($total_interactions); ?> total interactions</p>
                    <p><strong>Member Since:</strong> <?php echo $account_age_months; ?> months ago</p>
                    <p><strong>Account Status:</strong> 
                        <?php if ($is_verified): ?>
                            <span class="success">Verified Account</span>
                        <?php else: ?>
                            <span class="muted">Regular Account</span>
                        <?php endif; ?>
                    </p>
                </div>
            </div>
        </div>
    </main>
</body>
</html>
```

### Step 3: Understanding the PHP Syntax

**Key PHP Points:**

- **PHP Tags:** All PHP code must be inside `<?php ?>` tags
- **Variables:** Always start with `$` followed by the name (like `$username`)
- **String Concatenation:** Use the `.` operator to join strings
- **Comments:** Use `//` for single lines or `/* */` for multiple lines
- **Output:** `echo` displays content to the browser
- **Conditionals:** `if` statements work like other programming languages

---

## Complete Code

The complete code is shown above in the step-by-step implementation. The key files are:

1. **styles.css** - Shared dark theme styles for the entire chapter
2. **user-profile.php** - Dynamic user profile page demonstrating PHP variables

---

## Testing Your Work

### Quick Verification:

1. Save both files in the same directory on your web server
2. Open `user-profile.php` in your browser through your web server (like `http://localhost/user-profile.php`)
3. You should see a dark-themed profile page with Sarah Johnson's information
4. View the page source to see that PHP has been converted to HTML

### Troubleshooting:

**Issue:** Page shows PHP code instead of executing it  
**Fix:** Make sure you're accessing the file through a web server (localhost) not opening directly in browser

**Issue:** Styles don't load properly  
**Fix:** Ensure `styles.css` is in the same directory as `user-profile.php`

**Issue:** PHP errors displayed  
**Fix:** Check that all variables are defined before they're used with `echo`

---

## What You've Accomplished

✅ **Created your first PHP file** that combines server-side logic with HTML  
✅ **Learned PHP variable syntax** and how to store different data types  
✅ **Built a dynamic profile page** that displays user information  
✅ **Used conditional statements** to show/hide content based on data  
✅ **Established the dark theme** that will be used throughout the course

**Your platform can now:** Display dynamic user information that could easily be changed by modifying the PHP variables at the top of the file.

---

## Next Up

**Lesson 1.2:** Arrays & Loops - Displaying Posts and Users

We'll learn how to work with multiple pieces of data using PHP arrays and display them with loops - essential for showing lists of posts, users, and other social platform content.

---

## 💡 PHP Learning Notes

- **PHP is server-side:** Code runs on the server before HTML reaches the browser
- **Variables are flexible:** PHP automatically determines if a variable holds text, numbers, or other data
- **Security matters:** Always be careful about displaying user data (we'll learn more about this)
- **Separation of concerns:** Notice how we keep the data (variables) separate from the display (HTML)

This foundation will support everything we build in the coming lessons!
