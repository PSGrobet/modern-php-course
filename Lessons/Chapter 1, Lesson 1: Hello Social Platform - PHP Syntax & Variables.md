# Chapter 1, Lesson 1: Hello Social Platform - PHP Syntax & Variables

**Goal:** Create your first dynamic PHP page displaying user information for our social platform  
**Time:** 1-2 hours  
**Prerequisites:** Basic HTML knowledge, text editor installed  
**Files:** `hello-social.php`, `style.css`

---

## What You'll Learn

In this lesson, you will:

- Write your first PHP script with proper syntax
- Use variables to store user information
- Display dynamic content on a web page
- Understand how PHP integrates with HTML
- Create the foundation for our social platform project

---

## Why This Matters

Social platforms are built on dynamic content - user names, posts, profiles, and interactions that change based on who's logged in and what they're doing. Unlike static HTML pages that show the same content to everyone, PHP allows us to create pages that adapt to each user.

In this lesson, we're taking the first step toward building ConnectHub, our social platform. You'll learn how PHP variables store user information like names, usernames, and bio text - the building blocks of any social network profile.

By the end of this course, you'll have built a complete social platform where users can register, post content, follow each other, and interact. But it all starts here, with understanding how PHP stores and displays information dynamically.

---

## Core Concepts

### Concept 1: PHP Tags and Basic Syntax

**Definition:** PHP code must be wrapped in special tags that tell the web server "this is PHP code, please execute it."

**In Context:** When someone visits a profile page on our social platform, the server needs to know which parts are regular HTML (that stays the same) and which parts are PHP (that changes based on the user).

**Example:**

```php
<?php
// This is PHP code - it gets executed by the server
echo "Hello, World!";
?>

<!-- This is regular HTML - it stays the same -->
<p>This text never changes</p>
```

**Key Points:**

- PHP code starts with `<?php` and ends with `?>`
- Every PHP statement ends with a semicolon (`;`)
- Comments use `//` for single lines
- PHP executes on the server before the HTML reaches the user's browser

### Concept 2: Variables - Storing User Information

**Definition:** Variables are containers that hold information we want to use later, like a user's name or the number of posts they've made.

**In Context:** In our social platform, variables will store everything from usernames to post content to the number of likes on a photo.

**Example:**

```php
<?php
// Store user information in variables
$username = "sarah_dev";
$full_name = "Sarah Johnson";
$post_count = 42;
$is_verified = true;
?>
```

**Key Points:**

- Variables start with a dollar sign (`$`)
- Variable names are case-sensitive (`$username` is different from `$Username`)
- Use snake_case for variable names (`$full_name`, not `$fullName`)
- Variables can store text, numbers, true/false values, and more

### Concept 3: Displaying Variables in HTML

**Definition:** We use the `echo` statement to display variable content within our HTML, making our pages dynamic.

**In Context:** This is how we'll show each user their personalized profile information, their friends' posts, and customized content throughout our social platform.

**Example:**

```php
<?php
$username = "sarah_dev";
$followers = 1250;
?>

<h2>Welcome back, <?php echo $username; ?>!</h2>
<p>You have <?php echo $followers; ?> followers.</p>
```

**Key Points:**

- `echo` outputs the variable's value into the HTML
- You can mix PHP and HTML on the same page
- The user never sees the PHP code, only the final HTML result
- Variables can be displayed anywhere in your HTML structure

### Concept 4: String Concatenation

**Definition:** Combining multiple pieces of text and variables together to create longer messages.

**In Context:** We'll use this to create dynamic messages like "John posted 3 photos" or "Welcome back, Sarah! You have 5 new notifications."

**Example:**

```php
<?php
$username = "mike_photos";
$photo_count = 3;

// Combining text and variables
$message = "User " . $username . " has uploaded " . $photo_count . " photos today.";
echo $message;
?>
```

**Key Points:**

- The dot (`.`) operator joins text and variables together
- You can combine as many pieces as needed
- Spaces must be included in your text strings
- This creates personalized, dynamic content for each user

---

## Building It Step-by-Step

### Step 1: Create Your First Social Platform Page

**What we're doing:** Creating a dynamic profile preview that shows user information using PHP variables.

**The Code:**

Create a file named `hello-social.php`:

```php
<?php
/**
 * Social Platform Project - Chapter 1, Lesson 1
 * Our first dynamic social platform page showing user profile information
 */

// Store user profile information in variables
// In a real social platform, this data would come from a database
$username = "alex_coder";
$display_name = "Alex Rivera";
$bio = "Full-stack developer who loves building cool web apps";
$followers = 892;
$following = 156;
$posts = 47;
$is_verified = true;
$join_date = "March 2023";

// Calculate some dynamic information
// This shows how we can work with our variables
$total_connections = $followers + $following;
?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title><?php echo $display_name; ?> - ConnectHub Profile</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="container">
        <header class="profile-header">
            <!-- Display the user's name dynamically in the heading -->
            <h1>Welcome to <?php echo $display_name; ?>'s Profile</h1>

            <!-- Show verification badge if user is verified -->
            <?php if ($is_verified): ?>
                <span class="verified-badge">✓ Verified</span>
            <?php endif; ?>
        </header>

        <main class="profile-content">
            <div class="profile-info">
                <!-- Username with @ symbol like real social platforms -->
                <p class="username">@<?php echo $username; ?></p>

                <!-- User's bio text -->
                <p class="bio"><?php echo $bio; ?></p>

                <!-- Join date information -->
                <p class="join-date">Member since <?php echo $join_date; ?></p>
            </div>

            <div class="profile-stats">
                <h3>Profile Statistics</h3>

                <!-- Display follower count -->
                <div class="stat">
                    <strong><?php echo $followers; ?></strong> Followers
                </div>

                <!-- Display following count -->
                <div class="stat">
                    <strong><?php echo $following; ?></strong> Following
                </div>

                <!-- Display post count -->
                <div class="stat">
                    <strong><?php echo $posts; ?></strong> Posts
                </div>

                <!-- Show calculated total connections -->
                <div class="stat">
                    <strong><?php echo $total_connections; ?></strong> Total Connections
                </div>
            </div>

            <div class="dynamic-content">
                <h3>Dynamic Welcome Message</h3>

                <!-- Create a personalized message using string concatenation -->
                <p>
                    <?php 
                    echo "Hey there! " . $display_name . " has been active on ConnectHub since " . $join_date . ". ";
                    echo "With " . $followers . " followers and " . $posts . " posts, they're building a great community!";
                    ?>
                </p>

                <!-- Show different messages based on follower count -->
                <?php if ($followers > 500): ?>
                    <p class="achievement">🎉 Popular User Achievement Unlocked!</p>
                <?php else: ?>
                    <p class="encouragement">Keep posting to grow your follower count!</p>
                <?php endif; ?>
            </div>
        </main>

        <footer class="profile-footer">
            <p>This profile was generated dynamically with PHP on <?php echo date('F j, Y \a\t g:i A'); ?></p>
        </footer>
    </div>
</body>
</html>
```

**Understanding the Code:**

- **PHP Opening:** We start with `<?php` and our file comment explaining what this code does
- **Variable Declarations:** We create variables for all the user information we want to display
- **Calculations:** We show how to work with variables by adding followers + following
- **HTML Integration:** We use `<?php echo $variable; ?>` to display our data within the HTML
- **Conditional Display:** We use `if` statements to show different content based on the data
- **Dynamic Timestamps:** `date()` shows the current date and time when the page loads

**Testing It:** Save the file and open it in your browser. You should see a profile page with all the user information displayed dynamically.

### Step 2: Add CSS Styling

**What we're doing:** Making our social platform page look professional with CSS styling.

**The Code:**

Create a file named `style.css`:

```css
/**
 * Social Platform Styles - Chapter 1, Lesson 1
 * Basic styling for our profile page
 */

/* Reset and base styles */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    line-height: 1.6;
    color: #333;
    background-color: #f5f5f5;
}

/* Main container */
.container {
    max-width: 600px;
    margin: 20px auto;
    background: white;
    border-radius: 12px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    overflow: hidden;
}

/* Profile header styling */
.profile-header {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    padding: 30px;
    text-align: center;
    position: relative;
}

.profile-header h1 {
    font-size: 1.8rem;
    margin-bottom: 10px;
}

.verified-badge {
    background: #28a745;
    color: white;
    padding: 4px 8px;
    border-radius: 12px;
    font-size: 0.8rem;
    display: inline-block;
}

/* Profile content area */
.profile-content {
    padding: 30px;
}

.profile-info {
    text-align: center;
    margin-bottom: 30px;
    padding-bottom: 20px;
    border-bottom: 2px solid #eee;
}

.username {
    font-size: 1.2rem;
    color: #666;
    margin-bottom: 10px;
}

.bio {
    font-size: 1rem;
    color: #333;
    margin-bottom: 10px;
    font-style: italic;
}

.join-date {
    color: #888;
    font-size: 0.9rem;
}

/* Profile statistics */
.profile-stats {
    margin-bottom: 30px;
}

.profile-stats h3 {
    color: #333;
    margin-bottom: 20px;
    text-align: center;
}

.stat {
    display: flex;
    justify-content: space-between;
    padding: 10px 0;
    border-bottom: 1px solid #eee;
}

.stat:last-child {
    border-bottom: none;
}

.stat strong {
    color: #667eea;
}

/* Dynamic content section */
.dynamic-content {
    background: #f8f9fa;
    padding: 20px;
    border-radius: 8px;
    margin-bottom: 20px;
}

.dynamic-content h3 {
    color: #333;
    margin-bottom: 15px;
}

.achievement {
    background: #d4edda;
    color: #155724;
    padding: 10px;
    border-radius: 6px;
    border-left: 4px solid #28a745;
}

.encouragement {
    background: #fff3cd;
    color: #856404;
    padding: 10px;
    border-radius: 6px;
    border-left: 4px solid #ffc107;
}

/* Footer */
.profile-footer {
    background: #f8f9fa;
    padding: 15px 30px;
    text-align: center;
    color: #666;
    font-size: 0.8rem;
    border-top: 1px solid #eee;
}

/* Responsive design */
@media (max-width: 768px) {
    .container {
        margin: 10px;
        border-radius: 8px;
    }

    .profile-header {
        padding: 20px;
    }

    .profile-header h1 {
        font-size: 1.5rem;
    }

    .profile-content {
        padding: 20px;
    }
}
```

**Understanding the CSS:**

- **Professional Layout:** Clean, modern design that looks like real social platforms
- **Responsive Design:** Works on both desktop and mobile devices
- **Color Scheme:** Professional blues and grays with accent colors for achievements
- **Typography:** Clear, readable fonts with proper sizing hierarchy
- **Visual Hierarchy:** Different sections are clearly separated and organized

**Testing It:** Refresh your browser. Your profile page should now have professional styling that looks like a real social platform.

---

## Complete Code Files

### hello-social.php

```php
<?php
/**
 * Social Platform Project - Chapter 1, Lesson 1
 * Our first dynamic social platform page showing user profile information
 */

// Store user profile information in variables
// In a real social platform, this data would come from a database
$username = "alex_coder";
$display_name = "Alex Rivera";
$bio = "Full-stack developer who loves building cool web apps";
$followers = 892;
$following = 156;
$posts = 47;
$is_verified = true;
$join_date = "March 2023";

// Calculate some dynamic information
// This shows how we can work with our variables
$total_connections = $followers + $following;
?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title><?php echo $display_name; ?> - ConnectHub Profile</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="container">
        <header class="profile-header">
            <h1>Welcome to <?php echo $display_name; ?>'s Profile</h1>
            <?php if ($is_verified): ?>
                <span class="verified-badge">✓ Verified</span>
            <?php endif; ?>
        </header>

        <main class="profile-content">
            <div class="profile-info">
                <p class="username">@<?php echo $username; ?></p>
                <p class="bio"><?php echo $bio; ?></p>
                <p class="join-date">Member since <?php echo $join_date; ?></p>
            </div>

            <div class="profile-stats">
                <h3>Profile Statistics</h3>
                <div class="stat">
                    <strong><?php echo $followers; ?></strong> Followers
                </div>
                <div class="stat">
                    <strong><?php echo $following; ?></strong> Following
                </div>
                <div class="stat">
                    <strong><?php echo $posts; ?></strong> Posts
                </div>
                <div class="stat">
                    <strong><?php echo $total_connections; ?></strong> Total Connections
                </div>
            </div>

            <div class="dynamic-content">
                <h3>Dynamic Welcome Message</h3>
                <p>
                    <?php 
                    echo "Hey there! " . $display_name . " has been active on ConnectHub since " . $join_date . ". ";
                    echo "With " . $followers . " followers and " . $posts . " posts, they're building a great community!";
                    ?>
                </p>

                <?php if ($followers > 500): ?>
                    <p class="achievement">🎉 Popular User Achievement Unlocked!</p>
                <?php else: ?>
                    <p class="encouragement">Keep posting to grow your follower count!</p>
                <?php endif; ?>
            </div>
        </main>

        <footer class="profile-footer">
            <p>This profile was generated dynamically with PHP on <?php echo date('F j, Y \a\t g:i A'); ?></p>
        </footer>
    </div>
</body>
</html>
```

---

## Testing Your Work

### Quick Test Checklist:

- [ ] File opens in browser without errors
- [ ] User information displays correctly
- [ ] Verification badge appears
- [ ] Statistics show the correct numbers
- [ ] Dynamic message appears with user's information
- [ ] Achievement message shows (since followers > 500)
- [ ] Current date/time appears in footer
- [ ] Page is styled and looks professional

### Manual Testing:

1. **Open the file:** Navigate to `hello-social.php` in your browser
2. **Check dynamic content:** Verify that "Alex Rivera" and "@alex_coder" appear
3. **Modify variables:** Change `$followers` to 300 and refresh - achievement message should change
4. **Test responsiveness:** Resize your browser window to see mobile layout

### Troubleshooting Common Issues:

**Problem:** Page shows PHP code instead of executing it  
**Solution:** Make sure you're running this on a web server (XAMPP, WAMP, MAMP) and accessing it via `http://localhost/`, not opening the file directly in the browser.

**Problem:** CSS styling doesn't appear  
**Solution:** Ensure `style.css` is in the same folder as `hello-social.php` and the file names match exactly.

**Problem:** "Parse error" message appears  
**Solution:** Check that all PHP statements end with semicolons (`;`) and that all PHP tags are properly opened (`<?php`) and closed (`?>`).

---

## Project Progress Check

### What You've Built:

You've created your first dynamic social platform page that displays user profile information using PHP variables. The page shows a realistic user profile with statistics, bio information, and conditional content that changes based on the data.

### How It Fits:

This profile page demonstrates the foundation of any social platform - the ability to store and display user information dynamically. Every social network needs to show user profiles, and you've built the basic structure for that functionality.

### What's Working Now:

- Dynamic user profile display
- Conditional content (verification badges, achievement messages)
- Professional styling that looks like a real social platform
- Responsive design that works on mobile and desktop
- String concatenation for personalized messages

---

## Key Takeaways

After completing this lesson, you should understand:

- How PHP variables store different types of information (text, numbers, true/false values)
- How to use `echo` to display variable content within HTML
- How PHP tags (`<?php ?>`) separate server-side code from client-side HTML
- How to concatenate strings using the dot (`.`) operator to create dynamic messages
- How conditional statements (`if`) can show different content based on data values

---

## Next Up

**Coming in Lesson 1.2:** Data Types for Social Platforms - User Information

**You'll learn:** Different types of data that social platforms handle (strings, numbers, booleans, arrays) and how to work with user information like posts, comments, and friend lists.

**Files you'll work with:** You'll expand on `hello-social.php` to show different types of user data and create more sophisticated profile information.

---

## Additional Resources

### Quick References:

- [PHP Variables Documentation](https://www.php.net/manual/en/language.variables.php)
- [PHP echo Statement](https://www.php.net/manual/en/function.echo.php)
- [String Concatenation in PHP](https://www.php.net/manual/en/language.operators.string.php)

### Going Deeper:

- How major social platforms structure user data
- Introduction to web servers and how PHP executes
- Basic security considerations for displaying user data

---

## Chapter Progress

**Lessons Completed in Chapter 1:**

- [x] Lesson 1.1: Hello Social Platform - PHP Syntax & Variables
- [ ] Lesson 1.2: Data Types for Social Platforms - User Information
- [ ] Lesson 1.3: Arrays - Storing Multiple Users and Posts
- [ ] Lesson 1.4: Loops - Displaying Dynamic Content
- [ ] Lesson 1.5: Functions - Reusable Social Platform Tools

**Chapter Goal:** Master PHP basics while creating dynamic content for our social platform foundation.
