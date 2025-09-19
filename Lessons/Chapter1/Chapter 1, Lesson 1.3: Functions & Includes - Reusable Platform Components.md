# Chapter 1, Lesson 1.3: Functions & Includes - Reusable Platform Components

**Goal:** Organize code using PHP functions and includes to create reusable components for your social platform  
**Time:** 1-2 hours  
**Prerequisites:** Lessons 1.1-1.2 - PHP variables, arrays, and loops  
**New Code:** ~85 lines PHP across multiple files

---

## What You'll Build

In this lesson, you will:

- Create reusable PHP functions for common platform tasks
- Split code into separate files using `include` and `require`
- Build a shared header and navigation system
- Create utility functions for formatting and data processing
- Establish a modular structure that scales with your platform

---

## Why This Matters

As social platforms grow, code becomes complex quickly. Functions let you write code once and use it everywhere - format dates, display user info, calculate statistics. Includes let you organize code into logical files and avoid repetition across pages.

Professional PHP applications use hundreds of functions and dozens of included files. Learning to organize code properly from the beginning prevents the "spaghetti code" problem where everything becomes interconnected and hard to maintain.

---

## Core Concept: Functions and File Organization

**Definition:** Functions are reusable blocks of code that accept input, process it, and return results. Includes let you split code across multiple files and share common functionality.

**Syntax:**

```php
<?php
// Function definition
function format_post_date($timestamp) {
    return date('M j, Y \a\t g:i A', strtotime($timestamp));
}

// Function usage
$formatted_date = format_post_date('2024-01-15 14:30:00');

// Include external files
include 'header.php';        // Include once, warn if missing
require_once 'functions.php'; // Include once, error if missing
?>
```

**In Our Platform:** Functions will handle user display, date formatting, validation, and all repetitive tasks. Includes will organize navigation, headers, and shared components.

---

## Step-by-Step Implementation

### Step 1: Create Shared Functions File

**What we're doing:** Building utility functions that multiple pages can use

Create a file called `functions.php`:

```php
<?php
/**
 * Social Platform - Chapter 1, Lesson 1.3
 * Shared Functions - Reusable components for the platform
 */

/**
 * Format a user's display name with verification badge
 */
function display_user_name($name, $is_verified = false) {
    $output = htmlspecialchars($name);
    if ($is_verified) {
        $output .= ' <span style="color: #007acc;">✓</span>';
    }
    return $output;
}

/**
 * Format post timestamp into readable format
 */
function format_time_ago($timestamp) {
    // Simple time ago calculation
    $time_formats = [
        '1 minute ago', '2 minutes ago', '5 minutes ago', 
        '15 minutes ago', '30 minutes ago', '1 hour ago',
        '2 hours ago', '4 hours ago', '6 hours ago', '8 hours ago'
    ];

    // For demo purposes, return the timestamp as-is if it's already formatted
    if (strpos($timestamp, 'ago') !== false) {
        return $timestamp;
    }

    // Otherwise return a random time ago for demo
    return $time_formats[array_rand($time_formats)];
}

/**
 * Generate user avatar initials
 */
function get_user_initials($full_name) {
    $names = explode(' ', trim($full_name));
    $initials = '';

    foreach ($names as $name) {
        if (!empty($name)) {
            $initials .= strtoupper($name[0]);
            if (strlen($initials) >= 2) break; // Max 2 initials
        }
    }

    return $initials ?: '?';
}

/**
 * Calculate engagement rate for a post
 */
function calculate_engagement($likes, $comments, $shares = 0) {
    return $likes + ($comments * 2) + ($shares * 3);
}

/**
 * Format numbers with K/M suffixes
 */
function format_number($number) {
    if ($number >= 1000000) {
        return round($number / 1000000, 1) . 'M';
    } elseif ($number >= 1000) {
        return round($number / 1000, 1) . 'K';
    }
    return number_format($number);
}

/**
 * Truncate text to specified length
 */
function truncate_text($text, $length = 100) {
    if (strlen($text) <= $length) {
        return $text;
    }
    return substr($text, 0, $length) . '...';
}

/**
 * Display post engagement stats
 */
function display_post_stats($likes, $comments, $shares = 0) {
    $stats = [];

    if ($likes > 0) {
        $stats[] = "❤️ " . format_number($likes) . " likes";
    }
    if ($comments > 0) {
        $stats[] = "💬 " . format_number($comments) . " comments";
    }
    if ($shares > 0) {
        $stats[] = "🔄 " . format_number($shares) . " shares";
    }

    return implode(' • ', $stats);
}
?>
```

### Step 2: Create Shared Header Component

**What we're doing:** Building a reusable header that all pages can include

Create a file called `header.php`:

```php
<?php
/**
 * Social Platform - Chapter 1, Lesson 1.3
 * Shared Header Component
 */

// Make sure functions are available
require_once 'functions.php';

// Current user info (in real app, this would come from session/database)
$current_user = [
    'name' => 'Your Name',
    'username' => 'your_username',
    'avatar' => get_user_initials('Your Name'),
    'notifications' => 3
];

$page_title = isset($page_title) ? $page_title : 'Social Platform';
?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title><?php echo htmlspecialchars($page_title); ?></title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <nav class="nav">
        <div class="container flex">
            <div>
                <a href="dashboard.php" class="nav-link" style="font-weight: bold;">SocialHub</a>
                <a href="dashboard.php" class="nav-link">Feed</a>
                <a href="user-profile.php" class="nav-link">Profile</a>
                <a href="#" class="nav-link">Messages</a>
                <a href="#" class="nav-link">Search</a>
            </div>
            <div style="margin-left: auto;" class="flex">
                <?php if ($current_user['notifications'] > 0): ?>
                    <a href="#" class="nav-link">
                        🔔 <?php echo $current_user['notifications']; ?>
                    </a>
                <?php endif; ?>
                <a href="#" class="nav-link flex">
                    <div class="user-avatar" style="width: 25px; height: 25px; font-size: 12px;">
                        <?php echo $current_user['avatar']; ?>
                    </div>
                    <?php echo $current_user['username']; ?>
                </a>
            </div>
        </div>
    </nav>

    <main class="container">
```

### Step 3: Create Improved Dashboard Using Functions

**What we're doing:** Rebuilding the social feed using our new functions and includes

Create a file called `dashboard.php`:

```php
<?php
/**
 * Social Platform - Chapter 1, Lesson 1.3
 * Dashboard - Main social feed using functions and includes
 */

// Set page title for header
$page_title = 'Dashboard - Social Platform';

// Sample data (same as lesson 1.2 but we'll process it with functions)
$users = [
    ['id' => 1, 'username' => 'sarah_dev', 'name' => 'Sarah Johnson', 'verified' => true],
    ['id' => 2, 'username' => 'mike_codes', 'name' => 'Mike Chen', 'verified' => false],
    ['id' => 3, 'username' => 'alex_design', 'name' => 'Alex Rodriguez', 'verified' => true]
];

$posts = [
    [
        'id' => 1, 'user_id' => 1, 'likes' => 24, 'comments' => 8, 'shares' => 3,
        'content' => 'Just finished building my first PHP social platform! The functions and includes are making everything so much cleaner. 🚀',
        'timestamp' => '2024-01-15 14:30:00'
    ],
    [
        'id' => 2, 'user_id' => 2, 'likes' => 1200, 'comments' => 45, 'shares' => 12,
        'content' => 'PHP functions are game-changers! Writing reusable code feels so much more professional.',
        'timestamp' => '2024-01-15 12:15:00'
    ],
    [
        'id' => 3, 'user_id' => 3, 'likes' => 5600, 'comments' => 89, 'shares' => 23,
        'content' => 'Clean code principles in PHP: use functions, organize with includes, and always think about reusability! 👨‍💻',
        'timestamp' => '2024-01-15 10:45:00'
    ]
];

// Include header with navigation
include 'header.php';
?>

        <div class="card">
            <h1 class="title">Welcome Back!</h1>
            <p class="text">Here's what's happening in your network</p>
        </div>

        <!-- Loop through posts using our new functions -->
        <?php foreach ($posts as $post): ?>
            <?php 
            // Find post author using our existing logic
            $author = null;
            foreach ($users as $user) {
                if ($user['id'] == $post['user_id']) {
                    $author = $user;
                    break;
                }
            }
            ?>

            <article class="card">
                <div class="flex">
                    <div class="user-avatar">
                        <?php echo get_user_initials($author['name']); ?>
                    </div>
                    <div class="user-info">
                        <h3 style="margin: 0; color: #fff; font-size: 1rem;">
                            <?php echo display_user_name($author['name'], $author['verified']); ?>
                        </h3>
                        <p class="muted" style="margin: 0;">
                            @<?php echo $author['username']; ?> • <?php echo format_time_ago($post['timestamp']); ?>
                        </p>
                    </div>
                    <div style="margin-left: auto;" class="muted">
                        Engagement: <?php echo calculate_engagement($post['likes'], $post['comments'], $post['shares']); ?>
                    </div>
                </div>

                <div class="text" style="margin-top: 15px;">
                    <?php echo nl2br(htmlspecialchars($post['content'])); ?>
                </div>

                <div class="muted" style="margin-top: 15px;">
                    <?php echo display_post_stats($post['likes'], $post['comments'], $post['shares']); ?>
                </div>
            </article>
        <?php endforeach; ?>

        <!-- Quick stats using functions -->
        <div class="card">
            <h2 class="title">Platform Activity</h2>
            <div class="user-stats">
                <div class="stat">
                    <div class="stat-number"><?php echo count($posts); ?></div>
                    <div class="stat-label">Recent Posts</div>
                </div>
                <div class="stat">
                    <div class="stat-number"><?php echo count($users); ?></div>
                    <div class="stat-label">Active Users</div>
                </div>
                <div class="stat">
                    <div class="stat-number">
                        <?php 
                        $total_engagement = 0;
                        foreach ($posts as $post) {
                            $total_engagement += calculate_engagement($post['likes'], $post['comments'], $post['shares']);
                        }
                        echo format_number($total_engagement);
                        ?>
                    </div>
                    <div class="stat-label">Total Engagement</div>
                </div>
            </div>
        </div>

    </main>
</body>
</html>
```

---

## Testing Your Work

### Quick Verification:

1. Save all three new files: `functions.php`, `header.php`, and `dashboard.php`
2. Keep your existing `styles.css` from previous lessons
3. Open `http://localhost/dashboard.php` in your browser
4. You should see an improved dashboard with better navigation and formatted content
5. Notice how numbers are formatted with K/M suffixes and engagement is calculated

### Troubleshooting:

**Issue:** "Cannot include file" errors  
**Fix:** Make sure all files are in the same directory and filenames match exactly

**Issue:** Functions not working  
**Fix:** Ensure `functions.php` is included before any function calls

**Issue:** Header not displaying properly  
**Fix:** Check that `$page_title` is set before including `header.php`

---

## What You've Accomplished

✅ **Created reusable PHP functions** for common platform tasks  
✅ **Organized code into separate files** using includes  
✅ **Built a shared header component** that all pages can use  
✅ **Improved data formatting** with professional-looking numbers and engagement  
✅ **Established scalable code structure** that grows with your platform

**Your platform can now:** Reuse code efficiently, maintain consistency across pages, and handle formatting automatically with professional-looking results.

---

## Next Up

**Lesson 1.4:** Forms & User Input - Registration and Content Creation

We'll learn how to handle user input through HTML forms, process POST data, and validate user submissions - essential for any interactive platform.

---

## 💡 PHP Learning Notes

- **Functions prevent repetition:** Write once, use everywhere
- **Include vs Require:** Use `require_once` for critical files, `include` for optional ones
- **Function naming:** Use descriptive names that explain what the function does
- **Return values:** Functions should return processed data rather than echoing directly
- **File organization:** Logical separation makes code easier to maintain and debug

This modular approach is exactly how professional PHP applications are structured!
