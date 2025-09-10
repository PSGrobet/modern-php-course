# Chapter 1, Lesson 1: Hello Social Platform - PHP Syntax & Variables

**Goal:** Create your first dynamic PHP page that displays social platform content using variables  
**Time:** 90-120 minutes  
**Prerequisites:** Basic HTML knowledge and completed development environment setup  
**Files:** `index.php`, `styles.css`

---

## What You'll Learn

In this lesson, you will:

- Understand PHP syntax and how it integrates with HTML
- Master PHP variables and how to store user information
- Create your first dynamic social platform page
- Display user profiles and posts using PHP variables
- Connect PHP code to a clean, modern stylesheet

---

## Why This Matters

Social platforms are all about displaying dynamic content - user names, profile information, posts, and interactions that change based on who's logged in and what's happening on the platform. Unlike static HTML pages that always show the same content, PHP allows us to create pages that adapt and change.

In this lesson, you'll create the foundation of our social platform by learning how PHP can store and display information like usernames, profile details, and posts. This is the same concept used by Facebook when it shows your name at the top of the page, or when Twitter displays your personalized timeline.

Everything you learn here about variables and dynamic content will be essential as we build user registration, post creation, and all the interactive features that make a social platform engaging and personalized.

---

## Core Concepts

### Concept 1: PHP Syntax and Integration

**Definition:** PHP is a server-side programming language that runs before the HTML is sent to the user's browser. PHP code is written inside special tags that tell the server "process this as PHP code, not HTML."

**In Context:** When someone visits our social platform, the server processes all the PHP code first (like getting their username from a database), then sends the final HTML to their browser.

**Example:**

```php
<?php
// This is PHP code - it runs on the server
$welcome_message = "Welcome to ConnectHub!";
?>

<!DOCTYPE html>
<html>
<head>
    <title>Social Platform</title>
</head>
<body>
    <h1><?php echo $welcome_message; ?></h1>
    <!-- The browser sees: <h1>Welcome to ConnectHub!</h1> -->
</body>
</html>
```

**Key Points:**

- PHP code must be inside `<?php` and `?>` tags
- PHP runs on the server before HTML is sent to the browser
- Use `echo` to output PHP variables into HTML
- Mix PHP and HTML to create dynamic web pages

### Concept 2: PHP Variables

**Definition:** Variables are containers that store information. In PHP, all variables start with a dollar sign ($) followed by a name you choose.

**In Context:** Variables let us store user information like names, email addresses, post content, and profile details that we can use throughout our social platform.

**Example:**

```php
<?php
// Store user information in variables
$username = "john_doe";
$full_name = "John Doe";
$post_count = 42;
$is_verified = true;
?>
```

**Key Points:**

- Variables always start with $ in PHP
- Use snake_case for variable names (words_separated_by_underscores)
- Variables can store text, numbers, true/false values, and more
- Variable names should be descriptive and meaningful

### Concept 3: Data Types for Social Platforms

**Definition:** PHP has different types of data - strings (text), integers (whole numbers), floats (decimal numbers), and booleans (true/false).

**In Context:** Different types of social platform data require different data types - usernames are strings, follower counts are integers, account verification status is boolean.

**Example:**

```php
<?php
// Different data types for social platform features
$username = "sarah_wilson";        // String (text)
$follower_count = 1547;           // Integer (whole number)
$average_likes = 23.8;            // Float (decimal number)
$is_online = true;                // Boolean (true/false)
?>
```

**Key Points:**

- Strings hold text and must be in quotes ("" or '')
- Integers hold whole numbers with no quotes
- Floats hold decimal numbers
- Booleans hold only true or false (no quotes)

### Concept 4: Displaying Variables in HTML

**Definition:** The `echo` statement outputs the value of a PHP variable into the HTML, making it visible to users.

**In Context:** We use echo to display usernames in headers, show post content, display follower counts, and insert any dynamic information into our social platform pages.

**Example:**

```php
<?php
$user_name = "Alex Chen";
$bio = "Web developer and coffee enthusiast";
?>

<div class="user-profile">
    <h2><?php echo $user_name; ?></h2>
    <p><?php echo $bio; ?></p>
</div>
```

**Key Points:**

- Always use `echo` to output variables in HTML
- Variables inside echo don't need quotes around them
- You can echo variables anywhere in your HTML
- The browser sees the actual values, not the variable names

---

## Building It Step-by-Step

### Step 1: Create Your First PHP File

**What we're doing:** Setting up the basic structure of our social platform's homepage with PHP integration.

**The Code:**

Create a file called `index.php` in your project directory:

```php
<?php
/**
 * Social Platform Project - Chapter 1, Lesson 1
 * Homepage displaying user profiles and posts with PHP variables
 */

// User information variables
$current_user = "sarah_mitchell";
$full_name = "Sarah Mitchell";
$user_bio = "Digital artist and nature photographer";
$follower_count = 1247;
$following_count = 892;
$post_count = 156;
$is_verified = true;

// Sample post data
$latest_post = "Just captured the most amazing sunset at the lake! The colors were absolutely incredible. 🌅";
$post_likes = 23;
$post_time = "2 hours ago";
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ConnectHub - Social Platform</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header class="site-header">
        <div class="container">
            <h1 class="site-title">ConnectHub</h1>
            <nav class="main-nav">
                <span class="welcome-message">Welcome, <?php echo $full_name; ?>!</span>
            </nav>
        </div>
    </header>

    <main class="main-content">
        <div class="container">
            <section class="user-profile">
                <div class="profile-header">
                    <div class="profile-info">
                        <h2 class="username">
                            <?php echo $full_name; ?>
                            <?php if ($is_verified): ?>
                                <span class="verified-badge">✓</span>
                            <?php endif; ?>
                        </h2>
                        <p class="handle">@<?php echo $current_user; ?></p>
                        <p class="bio"><?php echo $user_bio; ?></p>
                    </div>
                </div>

                <div class="profile-stats">
                    <div class="stat">
                        <strong><?php echo $post_count; ?></strong>
                        <span>Posts</span>
                    </div>
                    <div class="stat">
                        <strong><?php echo $follower_count; ?></strong>
                        <span>Followers</span>
                    </div>
                    <div class="stat">
                        <strong><?php echo $following_count; ?></strong>
                        <span>Following</span>
                    </div>
                </div>
            </section>

            <section class="posts-section">
                <h3>Latest Posts</h3>

                <article class="post-card">
                    <header class="post-header">
                        <div class="post-author">
                            <strong><?php echo $full_name; ?></strong>
                            <span class="post-handle">@<?php echo $current_user; ?></span>
                            <span class="post-time"><?php echo $post_time; ?></span>
                        </div>
                    </header>

                    <div class="post-content">
                        <p><?php echo $latest_post; ?></p>
                    </div>

                    <footer class="post-actions">
                        <span class="like-count"><?php echo $post_likes; ?> likes</span>
                        <span class="comment-count">8 comments</span>
                        <span class="share-count">3 shares</span>
                    </footer>
                </article>
            </section>
        </div>
    </main>

    <footer class="site-footer">
        <div class="container">
            <p>© 2024 ConnectHub. Built with PHP by <?php echo $full_name; ?>!</p>
        </div>
    </footer>
</body>
</html>
```

**Understanding the Code:**

- **PHP Opening Tags:** `<?php` tells the server to start processing PHP code
- **Variables Declaration:** We store all our user information in descriptive variables at the top
- **HTML Integration:** PHP variables are echoed into the HTML using `<?php echo $variable_name; ?>`
- **Conditional Display:** The verified badge only shows if `$is_verified` is true
- **File Organization:** PHP logic at the top, HTML structure below

**Testing It:** Save the file and navigate to `http://localhost/your-project-folder/index.php` in your browser. You should see a social platform page with Sarah's profile information displayed dynamically.

### Step 2: Create the Stylesheet

**What we're doing:** Adding professional styling to make our social platform look modern and appealing.

**The Code:**

Create a file called `styles.css` in the same directory:

```css
/**
 * Social Platform Styles - Chapter 1, Lesson 1
 * Base styles for dynamic social platform layout
 */

/* Reset and Base Styles */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-size: 16px;
    line-height: 1.6;
    color: #333;
    background-color: #f8f9fa;
}

.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
}

/* Header Styles */
.site-header {
    background: #fff;
    border-bottom: 1px solid #e1e8ed;
    padding: 1rem 0;
    position: sticky;
    top: 0;
    z-index: 100;
}

.site-header .container {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.site-title {
    color: #1da1f2;
    font-size: 1.75rem;
    font-weight: bold;
}

.welcome-message {
    color: #657786;
    font-weight: 500;
}

/* Main Content */
.main-content {
    padding: 2rem 0;
}

/* User Profile Section */
.user-profile {
    background: #fff;
    border-radius: 12px;
    padding: 2rem;
    margin-bottom: 2rem;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.profile-header {
    margin-bottom: 1.5rem;
}

.username {
    font-size: 1.5rem;
    font-weight: bold;
    color: #14171a;
    display: flex;
    align-items: center;
    gap: 0.5rem;
}

.verified-badge {
    color: #1da1f2;
    font-size: 1.25rem;
}

.handle {
    color: #657786;
    font-size: 1rem;
    margin: 0.25rem 0;
}

.bio {
    color: #14171a;
    font-size: 1rem;
    margin-top: 0.75rem;
}

/* Profile Stats */
.profile-stats {
    display: flex;
    gap: 2rem;
    padding-top: 1rem;
    border-top: 1px solid #e1e8ed;
}

.stat {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
}

.stat strong {
    font-size: 1.25rem;
    font-weight: bold;
    color: #14171a;
}

.stat span {
    font-size: 0.875rem;
    color: #657786;
    text-transform: uppercase;
    letter-spacing: 0.5px;
}

/* Posts Section */
.posts-section {
    background: #fff;
    border-radius: 12px;
    padding: 2rem;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.posts-section h3 {
    color: #14171a;
    font-size: 1.25rem;
    margin-bottom: 1.5rem;
    padding-bottom: 0.5rem;
    border-bottom: 2px solid #1da1f2;
}

/* Post Card */
.post-card {
    border: 1px solid #e1e8ed;
    border-radius: 8px;
    padding: 1.5rem;
    margin-bottom: 1rem;
}

.post-header {
    margin-bottom: 1rem;
}

.post-author {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    flex-wrap: wrap;
}

.post-author strong {
    color: #14171a;
    font-weight: bold;
}

.post-handle {
    color: #657786;
}

.post-time {
    color: #657786;
    font-size: 0.875rem;
}

.post-content p {
    color: #14171a;
    font-size: 1rem;
    margin-bottom: 1rem;
    line-height: 1.5;
}

/* Post Actions */
.post-actions {
    display: flex;
    gap: 1.5rem;
    padding-top: 1rem;
    border-top: 1px solid #e1e8ed;
    font-size: 0.875rem;
    color: #657786;
}

/* Footer */
.site-footer {
    background: #fff;
    border-top: 1px solid #e1e8ed;
    padding: 2rem 0;
    text-align: center;
    color: #657786;
    margin-top: 3rem;
}

/* Responsive Design */
@media (max-width: 768px) {
    .container {
        padding: 0 15px;
    }

    .site-header .container {
        flex-direction: column;
        gap: 1rem;
        text-align: center;
    }

    .profile-stats {
        justify-content: space-around;
    }

    .post-author {
        flex-direction: column;
        align-items: flex-start;
        gap: 0.25rem;
    }
}
```

**Understanding the Code:**

- **Modern Design:** Clean, card-based layout similar to popular social platforms
- **Responsive:** Adapts to different screen sizes with media queries
- **Color Scheme:** Professional blue and gray color palette
- **Typography:** Clear, readable fonts with proper sizing hierarchy
- **Interactive Elements:** Hover effects and proper spacing for user interface elements

**Testing It:** Refresh your browser page. You should now see a beautifully styled social platform page that looks professional and modern.

### Step 3: Experimenting with Different Data

**What we're doing:** Modifying variables to see how dynamic content works and understanding the power of PHP variables.

**The Code:**

Try changing some variables at the top of your `index.php` file:

```php
<?php
// Try changing these values and refresh the page to see the differences!

// Change the user information
$current_user = "alex_developer";
$full_name = "Alex Rodriguez";
$user_bio = "Full-stack developer building the future of web applications";
$follower_count = 2847;
$following_count = 445;
$post_count = 89;
$is_verified = false; // Try changing this to true!

// Change the post content
$latest_post = "Just deployed my first PHP application! The feeling of seeing your code come to life is incredible. Thanks to everyone who helped me along the way! 🚀";
$post_likes = 156;
$post_time = "45 minutes ago";
?>
```

**Understanding the Code:** By changing just the variables at the top, the entire page updates automatically. This demonstrates the power of dynamic content - one change affects multiple places on the page.

**Testing It:** Save the file and refresh your browser. Notice how the entire page updates with Alex's information instead of Sarah's, and the verified badge disappears when you set `$is_verified` to false.

---

## Complete Code Files

### index.php

```php
<?php
/**
 * Social Platform Project - Chapter 1, Lesson 1
 * Homepage displaying user profiles and posts with PHP variables
 */

// User information variables
$current_user = "sarah_mitchell";
$full_name = "Sarah Mitchell";
$user_bio = "Digital artist and nature photographer";
$follower_count = 1247;
$following_count = 892;
$post_count = 156;
$is_verified = true;

// Sample post data
$latest_post = "Just captured the most amazing sunset at the lake! The colors were absolutely incredible. 🌅";
$post_likes = 23;
$post_time = "2 hours ago";
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ConnectHub - Social Platform</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header class="site-header">
        <div class="container">
            <h1 class="site-title">ConnectHub</h1>
            <nav class="main-nav">
                <span class="welcome-message">Welcome, <?php echo $full_name; ?>!</span>
            </nav>
        </div>
    </header>

    <main class="main-content">
        <div class="container">
            <section class="user-profile">
                <div class="profile-header">
                    <div class="profile-info">
                        <h2 class="username">
                            <?php echo $full_name; ?>
                            <?php if ($is_verified): ?>
                                <span class="verified-badge">✓</span>
                            <?php endif; ?>
                        </h2>
                        <p class="handle">@<?php echo $current_user; ?></p>
                        <p class="bio"><?php echo $user_bio; ?></p>
                    </div>
                </div>

                <div class="profile-stats">
                    <div class="stat">
                        <strong><?php echo $post_count; ?></strong>
                        <span>Posts</span>
                    </div>
                    <div class="stat">
                        <strong><?php echo $follower_count; ?></strong>
                        <span>Followers</span>
                    </div>
                    <div class="stat">
                        <strong><?php echo $following_count; ?></strong>
                        <span>Following</span>
                    </div>
                </div>
            </section>

            <section class="posts-section">
                <h3>Latest Posts</h3>

                <article class="post-card">
                    <header class="post-header">
                        <div class="post-author">
                            <strong><?php echo $full_name; ?></strong>
                            <span class="post-handle">@<?php echo $current_user; ?></span>
                            <span class="post-time"><?php echo $post_time; ?></span>
                        </div>
                    </header>

                    <div class="post-content">
                        <p><?php echo $latest_post; ?></p>
                    </div>

                    <footer class="post-actions">
                        <span class="like-count"><?php echo $post_likes; ?> likes</span>
                        <span class="comment-count">8 comments</span>
                        <span class="share-count">3 shares</span>
                    </footer>
                </article>
            </section>
        </div>
    </main>

    <footer class="site-footer">
        <div class="container">
            <p>© 2024 ConnectHub. Built with PHP by <?php echo $full_name; ?>!</p>
        </div>
    </footer>
</body>
</html>
```

### styles.css

```css
/**
 * Social Platform Styles - Chapter 1, Lesson 1
 * Base styles for dynamic social platform layout
 */

/* Reset and Base Styles */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-size: 16px;
    line-height: 1.6;
    color: #333;
    background-color: #f8f9fa;
}

.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
}

/* Header Styles */
.site-header {
    background: #fff;
    border-bottom: 1px solid #e1e8ed;
    padding: 1rem 0;
    position: sticky;
    top: 0;
    z-index: 100;
}

.site-header .container {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.site-title {
    color: #1da1f2;
    font-size: 1.75rem;
    font-weight: bold;
}

.welcome-message {
    color: #657786;
    font-weight: 500;
}

/* Main Content */
.main-content {
    padding: 2rem 0;
}

/* User Profile Section */
.user-profile {
    background: #fff;
    border-radius: 12px;
    padding: 2rem;
    margin-bottom: 2rem;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.profile-header {
    margin-bottom: 1.5rem;
}

.username {
    font-size: 1.5rem;
    font-weight: bold;
    color: #14171a;
    display: flex;
    align-items: center;
    gap: 0.5rem;
}

.verified-badge {
    color: #1da1f2;
    font-size: 1.25rem;
}

.handle {
    color: #657786;
    font-size: 1rem;
    margin: 0.25rem 0;
}

.bio {
    color: #14171a;
    font-size: 1rem;
    margin-top: 0.75rem;
}

/* Profile Stats */
.profile-stats {
    display: flex;
    gap: 2rem;
    padding-top: 1rem;
    border-top: 1px solid #e1e8ed;
}

.stat {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
}

.stat strong {
    font-size: 1.25rem;
    font-weight: bold;
    color: #14171a;
}

.stat span {
    font-size: 0.875rem;
    color: #657786;
    text-transform: uppercase;
    letter-spacing: 0.5px;
}

/* Posts Section */
.posts-section {
    background: #fff;
    border-radius: 12px;
    padding: 2rem;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.posts-section h3 {
    color: #14171a;
    font-size: 1.25rem;
    margin-bottom: 1.5rem;
    padding-bottom: 0.5rem;
    border-bottom: 2px solid #1da1f2;
}

/* Post Card */
.post-card {
    border: 1px solid #e1e8ed;
    border-radius: 8px;
    padding: 1.5rem;
    margin-bottom: 1rem;
}

.post-header {
    margin-bottom: 1rem;
}

.post-author {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    flex-wrap: wrap;
}

.post-author strong {
    color: #14171a;
    font-weight: bold;
}

.post-handle {
    color: #657786;
}

.post-time {
    color: #657786;
    font-size: 0.875rem;
}

.post-content p {
    color: #14171a;
    font-size: 1rem;
    margin-bottom: 1rem;
    line-height: 1.5;
}

/* Post Actions */
.post-actions {
    display: flex;
    gap: 1.5rem;
    padding-top: 1rem;
    border-top: 1px solid #e1e8ed;
    font-size: 0.875rem;
    color: #657786;
}

/* Footer */
.site-footer {
    background: #fff;
    border-top: 1px solid #e1e8ed;
    padding: 2rem 0;
    text-align: center;
    color: #657786;
    margin-top: 3rem;
}

/* Responsive Design */
@media (max-width: 768px) {
    .container {
        padding: 0 15px;
    }

    .site-header .container {
        flex-direction: column;
        gap: 1rem;
        text-align: center;
    }

    .profile-stats {
        justify-content: space-around;
    }

    .post-author {
        flex-direction: column;
        align-items: flex-start;
        gap: 0.25rem;
    }
}
```

---

## Testing Your Work

### Quick Test Checklist:

- [ ] PHP file loads without errors at `http://localhost/your-project-folder/index.php`
- [ ] All user information displays correctly (name, handle, bio, stats)
- [ ] Verified badge appears when `$is_verified` is true
- [ ] Post content and engagement numbers show properly
- [ ] Page looks professional with clean styling
- [ ] Page is responsive on mobile devices

### Manual Testing:

1. **Load the page** - Navigate to your index.php file in the browser
2. **Check dynamic content** - Verify that all PHP variables appear as content, not as code
3. **Test variable changes** - Modify some variables and refresh to see changes
4. **Verify styling** - Confirm the page looks professional and modern
5. **Test responsiveness** - Resize your browser window to test mobile layout

### Troubleshooting Common Issues:

**Problem:** Page shows PHP code instead of processing it  
**Solution:** Make sure you're accessing the page through localhost (http://localhost/your-project/) not by opening the file directly. PHP requires a web server to process.

**Problem:** CSS styles aren't loading  
**Solution:** Verify that styles.css is in the same directory as index.php and check the file name spelling in the HTML link tag.

**Problem:** Variables aren't displaying  
**Solution:** Check that each variable is properly defined with the $ symbol and that you're using `<?php echo $variable_name; ?>` in the HTML.

---

## Project Progress Check

### What You've Built:

You've created a dynamic social platform homepage that displays user profile information, statistics, and posts using PHP variables. The page looks professional and responds to different screen sizes.

### How It Fits:

This foundation page demonstrates the core concept of dynamic content that drives all social platforms. You now understand how PHP can generate personalized content for each user.

### What's Working Now:

- Dynamic user profile display with name, handle, and bio
- Profile statistics showing posts, followers, and following counts
- Conditional verified badge display
- Sample post with engagement metrics
- Professional, responsive design
- PHP and HTML integration

---

## Key Takeaways

After completing this lesson, you should understand:

- PHP code is written inside `<?php ?>` tags and runs on the server before HTML is sent to browsers
- Variables in PHP start with $ and can store different types of data (strings, numbers, booleans)
- The `echo` statement outputs variable values into HTML to create dynamic content
- PHP variables can be used anywhere in HTML to personalize content for users
- Proper variable naming (snake_case) and organization makes code easier to read and maintain

---

## Next Up

**Coming in Lesson 1.2:** Data Types for Social Platforms - User Information

**You'll learn:** How to work with different data types, organize user information more effectively, and handle more complex social platform data like arrays and user preferences.

**Files you'll work with:** `user-data.php`, expanded `index.php`

---

## Additional Resources

### Quick References:

- [PHP Variables Documentation](https://www.php.net/manual/en/language.variables.php)
- [PHP Data Types](https://www.php.net/manual/en/language.types.php)
- [PHP Echo Statement](https://www.php.net/manual/en/function.echo.php)

### Going Deeper:

- Variable scope and global variables
- String concatenation and manipulation
- PHP configuration and error reporting

---

## Chapter Progress

**Lessons Completed in Chapter 1:**

- [x] Lesson 1.1: Hello Social Platform - PHP Syntax & Variables
- [ ] Lesson 1.2: Data Types for Social Platforms - User Information
- [ ] Lesson 1.3: Arrays - Storing Multiple Users and Posts
- [ ] Lesson 1.4: Loops - Displaying Dynamic Content
- [ ] Lesson 1.5: Functions - Reusable Social Platform Tools

**Chapter Goal:** Master PHP foundations while creating dynamic social platform content
