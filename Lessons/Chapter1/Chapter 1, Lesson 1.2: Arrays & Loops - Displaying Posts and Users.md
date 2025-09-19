# Chapter 1, Lesson 1.2: Arrays & Loops - Displaying Posts and Users

**Goal:** Master PHP arrays and loops by building a social platform feed that displays multiple posts and users  
**Time:** 1-2 hours  
**Prerequisites:** Lesson 1.1 - PHP variables and basic syntax  
**New Code:** ~95 lines PHP/HTML

---

## What You'll Build

In this lesson, you will:

- Create PHP arrays to store multiple posts and users
- Use `foreach` loops to display repeating content
- Build a social platform feed showing posts from different users
- Learn array structure and accessing array data
- Display dynamic lists that could easily come from a database

---

## Why This Matters

Social platforms are built on lists of data - posts in a feed, users to follow, comments on posts, notifications, and more. PHP arrays let us store and organize multiple pieces of related information, while loops let us display each item consistently.

Understanding arrays and loops is crucial because real social platforms handle hundreds or thousands of posts, users, and interactions. The patterns you learn here scale directly to database-driven applications where arrays hold query results.

---

## Core Concept: PHP Arrays and Loops

**Definition:** PHP arrays store multiple values in a single variable. You can access individual items or loop through all items to perform the same action on each one.

**Syntax:**

```php
<?php
// Simple array (indexed)
$usernames = ['john_doe', 'sarah_dev', 'mike_codes'];

// Associative array (key-value pairs)  
$user = [
    'username' => 'john_doe',
    'name' => 'John Smith',
    'posts' => 42
];

// Array of arrays (like database rows)
$posts = [
    ['title' => 'First Post', 'author' => 'John'],
    ['title' => 'Second Post', 'author' => 'Sarah']
];

// Loop through arrays
foreach ($posts as $post) {
    echo $post['title']; // Access array values
}
?>
```

**In Our Platform:** Arrays will store posts, users, comments, and all the structured data that makes up a social platform's content.

---

## Step-by-Step Implementation

### Step 1: Create Sample Data Arrays

**What we're doing:** Setting up arrays that simulate what we'd get from a database - multiple posts and users

Create a file called `social-feed.php`:

```php
<?php
/**
 * Social Platform - Chapter 1, Lesson 1.2
 * Social Feed - Demonstrates PHP arrays and loops
 */

// Array of users - simulates user database table
$users = [
    [
        'id' => 1,
        'username' => 'sarah_dev',
        'name' => 'Sarah Johnson',
        'avatar' => 'SJ',
        'verified' => true
    ],
    [
        'id' => 2,
        'username' => 'mike_codes',
        'name' => 'Mike Chen',
        'avatar' => 'MC',
        'verified' => false
    ],
    [
        'id' => 3,
        'username' => 'alex_design',
        'name' => 'Alex Rodriguez',
        'avatar' => 'AR',
        'verified' => true
    ]
];

// Array of posts - simulates posts database table
$posts = [
    [
        'id' => 1,
        'user_id' => 1,
        'content' => 'Just finished building my first PHP social platform! The array and loop concepts are really clicking now. 🚀',
        'timestamp' => '2 hours ago',
        'likes' => 24,
        'comments' => 8
    ],
    [
        'id' => 2,
        'user_id' => 2,
        'content' => 'Anyone else love how PHP arrays work? Coming from other languages, the flexibility is amazing. Working on a new project using associative arrays.',
        'timestamp' => '4 hours ago',
        'likes' => 15,
        'comments' => 3
    ],
    [
        'id' => 3,
        'user_id' => 3,
        'content' => 'Design tip: When building social platforms, keep the UI simple and focus on the content. Dark themes are great for reducing eye strain! 👨‍💻',
        'timestamp' => '6 hours ago',
        'likes' => 42,
        'comments' => 12
    ],
    [
        'id' => 4,
        'user_id' => 1,
        'content' => 'Learning PHP has been such a journey. Arrays and loops make handling data so much easier than I expected!',
        'timestamp' => '8 hours ago',
        'likes' => 18,
        'comments' => 5
    ]
];

// Function to find user by ID
function find_user_by_id($users, $user_id) {
    foreach ($users as $user) {
        if ($user['id'] == $user_id) {
            return $user;
        }
    }
    return null;
}
?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Social Feed - Social Platform</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <nav class="nav">
        <div class="container">
            <a href="user-profile.php" class="nav-link">Profile</a>
            <a href="social-feed.php" class="nav-link">Feed</a>
            <a href="#" class="nav-link">Messages</a>
            <a href="#" class="nav-link">Settings</a>
        </div>
    </nav>

    <main class="container">
        <div class="card">
            <h1 class="title">Social Feed</h1>
            <p class="text">Latest posts from your network</p>
        </div>

        <!-- Loop through posts and display each one -->
        <?php foreach ($posts as $post): ?>
            <?php 
            // Find the user who made this post
            $post_author = find_user_by_id($users, $post['user_id']);
            ?>

            <article class="card">
                <div class="flex">
                    <div class="user-avatar">
                        <?php echo $post_author['avatar']; ?>
                    </div>
                    <div class="user-info">
                        <h3 style="margin: 0; color: #fff; font-size: 1rem;">
                            <?php echo $post_author['name']; ?>
                            <?php if ($post_author['verified']): ?>
                                <span style="color: #007acc;">✓</span>
                            <?php endif; ?>
                        </h3>
                        <p class="muted" style="margin: 0;">
                            @<?php echo $post_author['username']; ?> • <?php echo $post['timestamp']; ?>
                        </p>
                    </div>
                </div>

                <div class="text" style="margin-top: 15px;">
                    <?php echo nl2br($post['content']); ?>
                </div>

                <div class="flex" style="margin-top: 15px; gap: 20px;">
                    <span class="muted">❤️ <?php echo $post['likes']; ?> likes</span>
                    <span class="muted">💬 <?php echo $post['comments']; ?> comments</span>
                    <span class="muted">🔄 Share</span>
                </div>
            </article>
        <?php endforeach; ?>

        <!-- Display users to follow -->
        <div class="card">
            <h2 class="title">Suggested Users</h2>
            <p class="text">Connect with other developers</p>

            <?php foreach ($users as $user): ?>
                <div class="flex" style="margin: 15px 0; padding: 10px; background: #1a1a1a; border-radius: 5px;">
                    <div class="user-avatar" style="width: 40px; height: 40px;">
                        <?php echo $user['avatar']; ?>
                    </div>
                    <div class="user-info">
                        <h4 style="margin: 0; color: #fff; font-size: 0.9rem;">
                            <?php echo $user['name']; ?>
                            <?php if ($user['verified']): ?>
                                <span style="color: #007acc;">✓</span>
                            <?php endif; ?>
                        </h4>
                        <p class="muted" style="margin: 0;">@<?php echo $user['username']; ?></p>
                    </div>
                    <div style="margin-left: auto;">
                        <a href="#" class="btn" style="padding: 5px 10px; font-size: 12px;">Follow</a>
                    </div>
                </div>
            <?php endforeach; ?>
        </div>

        <!-- Display some array statistics -->
        <div class="card">
            <h2 class="title">Platform Statistics</h2>
            <div class="user-stats">
                <div class="stat">
                    <div class="stat-number"><?php echo count($posts); ?></div>
                    <div class="stat-label">Total Posts</div>
                </div>
                <div class="stat">
                    <div class="stat-number"><?php echo count($users); ?></div>
                    <div class="stat-label">Active Users</div>
                </div>
                <div class="stat">
                    <div class="stat-number">
                        <?php 
                        // Calculate total likes across all posts
                        $total_likes = 0;
                        foreach ($posts as $post) {
                            $total_likes += $post['likes'];
                        }
                        echo $total_likes;
                        ?>
                    </div>
                    <div class="stat-label">Total Likes</div>
                </div>
            </div>
        </div>
    </main>
</body>
</html>
```

### Step 2: Understanding Array Structure

**Key PHP Points:**

- **Indexed Arrays:** Use numbers as keys (0, 1, 2, ...)
- **Associative Arrays:** Use strings as keys ('name', 'username', 'posts')
- **Multidimensional Arrays:** Arrays containing other arrays (like database rows)
- **Array Access:** Use square brackets `$array['key']` or `$array[0]`
- **foreach Loop:** Best way to iterate through all array items

### Step 3: Working with Complex Data

**What we're demonstrating:** How to connect related data (like posts to their authors)

The `find_user_by_id()` function shows how to search through arrays to find related information, simulating what we'll later do with database joins.

---

## Testing Your Work

### Quick Verification:

1. Save `social-feed.php` in the same directory as your `styles.css` from Lesson 1.1
2. Open `http://localhost/social-feed.php` in your browser
3. You should see a social feed with 4 posts from 3 different users
4. Notice how each post shows the correct author information
5. Scroll down to see the suggested users and platform statistics

### Troubleshooting:

**Issue:** "Undefined index" errors  
**Fix:** Make sure all array keys match exactly (case-sensitive)

**Issue:** Posts show but no user information  
**Fix:** Check that the `find_user_by_id()` function is working correctly

**Issue:** Loops not displaying anything  
**Fix:** Verify that your arrays have data and are properly formatted

---

## What You've Accomplished

✅ **Created complex PHP arrays** that store multiple users and posts  
✅ **Used foreach loops** to display repeating content efficiently  
✅ **Built a working social feed** with posts from different authors  
✅ **Connected related data** by linking posts to users  
✅ **Calculated statistics** from array data using loops

**Your platform can now:** Display multiple posts and users in an organized, scalable way that mirrors how real social platforms work with database data.

---

## Next Up

**Lesson 1.3:** Functions & Includes - Reusable Platform Components

We'll learn how to organize code into reusable functions and separate files, making our platform more maintainable and professional.

---

## 💡 PHP Learning Notes

- **Arrays are flexible:** Can store any type of data and mix different types
- **Associative arrays:** Perfect for structured data like user profiles or posts
- **foreach vs for:** Use `foreach` for arrays, `for` for counted loops
- **Array functions:** PHP has many built-in functions like `count()` for working with arrays
- **Real-world connection:** This array structure directly matches database query results

This lesson establishes the data handling patterns you'll use throughout the entire course!
