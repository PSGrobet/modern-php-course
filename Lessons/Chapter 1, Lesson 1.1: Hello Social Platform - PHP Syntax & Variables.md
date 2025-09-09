# Chapter 1, Lesson 1.1: Hello Social Platform - PHP Syntax & Variables

**Goal:** Master PHP basics by creating your first dynamic social platform page with user information  
**Time:** 1-2 hours  
**Prerequisites:** Basic HTML knowledge, text editor installed, local server running (XAMPP/MAMP)  
**Files:** `hello-social.php` (new file you'll create)

---

## What You'll Learn

In this lesson, you will:

- Write your first PHP code that displays dynamic content
- Master PHP syntax rules and best practices
- Use variables to store and display user information
- Understand how PHP integrates with HTML
- Create the foundation for your social platform project

---

## Why This Matters

Every social platform starts with displaying user information dynamically. Whether it's Facebook showing your name, Twitter displaying your bio, or Instagram showing your follower count - it all begins with PHP variables storing and displaying data.

In this lesson, you'll learn the fundamental building blocks that power every feature of a social platform. Variables in PHP are like containers that hold information about users, posts, likes, and everything else that makes a social network work.

This is where your journey from beginner to building real web applications begins. By the end of this course, you'll have built a complete social platform, but it all starts here with understanding how to store and display information using PHP variables.

---

## Core Concepts

### Concept 1: What is PHP and Why Do We Use It?

**Definition:** PHP is a server-side programming language that runs on the web server before the page is sent to the user's browser.

**In Context:** When someone visits your social platform, PHP processes their request (like loading their profile or timeline) and generates the HTML that their browser displays.

**Example:**

```php
<?php
// This code runs on the server
$user_name = "Sarah Johnson";
echo "Welcome to ConnectHub, " . $user_name . "!";
?>
```

**Key Points:**

- PHP code is written between `<?php` and `?>` tags
- PHP runs on the server, not in the user's browser
- PHP generates HTML that browsers can understand
- Social platforms use PHP to create personalized experiences

### Concept 2: Variables - Storing User Information

**Definition:** Variables are containers that store data like usernames, email addresses, post content, and other information your social platform needs.

**In Context:** Every piece of information on a social platform - your name, profile picture, posts, followers - starts as data stored in variables.

**Example:**

```php
<?php
// Variables for a user profile
$user_name = "Alex Chen";
$follower_count = 1248;
$bio = "Web developer and coffee enthusiast";
$is_verified = true;
?>
```

**Key Points:**

- Variable names start with a dollar sign `$`
- Use snake_case for variable names (like `$user_name`, not `$userName`)
- Variables can store text, numbers, and true/false values
- Choose descriptive names that explain what the data represents

### Concept 3: Data Types for Social Platforms

**Definition:** Different types of information (strings for text, integers for numbers, booleans for true/false) require different data types.

**In Context:** Your social platform will handle many types of data - text posts, like counts, verification status, timestamps - each needs the right data type.

**Example:**

```php
<?php
// String - text information
$post_content = "Just launched my new website!";

// Integer - whole numbers
$like_count = 47;

// Boolean - true or false
$is_online = true;

// Float - numbers with decimals
$account_balance = 29.99;
?>
```

**Key Points:**

- Strings (text) go in quotes: `"Hello World"`
- Integers are whole numbers: `42`, `1000`, `0`
- Booleans are `true` or `false` (no quotes)
- PHP is flexible with data types but being explicit helps prevent bugs

### Concept 4: Displaying Variables with Echo

**Definition:** The `echo` statement outputs variables and text to the web page that users see.

**In Context:** Everything users see on your social platform - usernames, post content, notifications - is displayed using `echo` or similar output functions.

**Example:**

```php
<?php
$user_name = "Maria Garcia";
$post_count = 156;

echo "Profile: " . $user_name;
echo "<br>"; // HTML line break
echo "Total Posts: " . $post_count;
?>
```

**Key Points:**

- `echo` displays variables and text on the web page
- Use the dot `.` to combine (concatenate) variables with text
- You can include HTML tags in echo statements
- Each `echo` statement can display multiple pieces of information

---

## Building It Step-by-Step

### Step 1: Create Your First PHP File

**What we're doing:** Setting up the basic structure for a social platform user profile page.

**The Code:**

Create a new file called `hello-social.php` in your web server directory:

```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ConnectHub - User Profile</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f5f5f5;
        }
        .profile-card {
            background: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        .profile-header {
            border-bottom: 1px solid #eee;
            padding-bottom: 20px;
            margin-bottom: 20px;
        }
        .stat {
            display: inline-block;
            margin-right: 30px;
            text-align: center;
        }
        .stat-number {
            font-size: 24px;
            font-weight: bold;
            color: #1877f2;
        }
        .stat-label {
            color: #666;
            font-size: 14px;
        }
    </style>
</head>
<body>
    <div class="profile-card">
        <?php
        /**
         * Social Platform Project - Chapter 1, Lesson 1.1
         * Basic user profile display using PHP variables
         */

        // User information variables
        $user_name = "Sarah Johnson";
        $username = "sarahj_designer";
        $bio = "UX Designer | Coffee lover | Dog mom 🐕";
        $follower_count = 1248;
        $following_count = 892;
        $post_count = 156;
        $is_verified = true;
        $is_online = true;

        // Display the profile header
        echo "<div class='profile-header'>";
        echo "<h1>" . $user_name;

        // Show verification badge if user is verified
        if ($is_verified) {
            echo " ✓";
        }
        echo "</h1>";

        echo "<p>@" . $username . "</p>";
        echo "<p>" . $bio . "</p>";
        echo "</div>";
        ?>
    </div>
</body>
</html>
```

**Understanding the Code:**

- We start with standard HTML structure for a web page
- CSS styles make our profile look like a real social platform
- PHP code goes between `<?php` and `?>` tags
- Variables store all the user information we want to display
- `echo` statements output the variables as HTML that browsers can show
- We use concatenation (the `.` operator) to combine text and variables

**Testing It:** Save the file and visit `http://localhost/hello-social.php` in your browser. You should see a profile card with Sarah's information.

### Step 2: Add Profile Statistics

**What we're doing:** Displaying follower counts and other social platform statistics using variables.

Add this PHP code after the bio display in your existing file:

```php
<?php
// Display profile statistics
echo "<div class='profile-stats'>";

echo "<div class='stat'>";
echo "<div class='stat-number'>" . $post_count . "</div>";
echo "<div class='stat-label'>Posts</div>";
echo "</div>";

echo "<div class='stat'>";
echo "<div class='stat-number'>" . $follower_count . "</div>";
echo "<div class='stat-label'>Followers</div>";
echo "</div>";

echo "<div class='stat'>";
echo "<div class='stat-number'>" . $following_count . "</div>";
echo "<div class='stat-label'>Following</div>";
echo "</div>";

echo "</div>";
?>
```

**Understanding the Code:** Each statistic is displayed using the same pattern - we echo HTML with the variable values inside. This creates the typical social media profile stats you see on every platform.

**Testing It:** Refresh your browser page. You should now see the post, follower, and following counts displayed in a nice row.

### Step 3: Add User Status Display

**What we're doing:** Using boolean variables to show if a user is online and display different messages based on their status.

Add this PHP code after the statistics:

```php
<?php
// Display user status
echo "<div class='user-status' style='margin-top: 20px; padding: 15px; background: #f8f9fa; border-radius: 5px;'>";

echo "<h3>Account Status</h3>";

// Show online status
if ($is_online) {
    echo "<p style='color: green;'>🟢 Currently Online</p>";
} else {
    echo "<p style='color: gray;'>⚫ Offline</p>";
}

// Show verification status
if ($is_verified) {
    echo "<p style='color: blue;'>✅ Verified Account</p>";
} else {
    echo "<p style='color: orange;'>⚠️ Unverified Account</p>";
}

echo "</div>";
?>
```

**Understanding the Code:**

- We use `if` statements to check boolean (true/false) variables
- Different messages display based on whether `$is_online` and `$is_verified` are true or false
- This shows how social platforms display different statuses for different users

**Testing It:** Refresh the page. You should see online and verification status messages.

### Step 4: Experiment with Different Users

**What we're doing:** Changing the variable values to see how the page updates automatically.

**The Code:**

Replace the user information variables at the top of your PHP section with these different examples:

```php
<?php
// Try this user - a new creator
$user_name = "Alex Chen";
$username = "alexcodes";
$bio = "Full-stack developer | Building the future one line of code at a time";
$follower_count = 42;
$following_count = 127;
$post_count = 8;
$is_verified = false;
$is_online = false;

// Or try this user - a popular influencer
/*
$user_name = "Emma Rodriguez";
$username = "emma_travels";
$bio = "Travel photographer | 📸 Capturing moments around the world";
$follower_count = 15420;
$following_count = 2341;
$post_count = 987;
$is_verified = true;
$is_online = true;
*/
?>
```

**Understanding the Code:**

- By changing just the variable values, the entire page updates
- This demonstrates the power of variables - change the data once, and it updates everywhere
- Comments (lines starting with `//` or between `/*` and `*/`) let you keep alternative code without running it

**Testing It:** Try different combinations of values. Change `$is_verified` from `false` to `true` and see how the verification badge appears.

---

## Complete Code Files

### hello-social.php

```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ConnectHub - User Profile</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f5f5f5;
        }
        .profile-card {
            background: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        .profile-header {
            border-bottom: 1px solid #eee;
            padding-bottom: 20px;
            margin-bottom: 20px;
        }
        .stat {
            display: inline-block;
            margin-right: 30px;
            text-align: center;
        }
        .stat-number {
            font-size: 24px;
            font-weight: bold;
            color: #1877f2;
        }
        .stat-label {
            color: #666;
            font-size: 14px;
        }
    </style>
</head>
<body>
    <div class="profile-card">
        <h2>Welcome to ConnectHub!</h2>
        <p>Your journey into social platform development starts here.</p>

        <?php
        /**
         * Social Platform Project - Chapter 1, Lesson 1.1
         * Basic user profile display using PHP variables
         */

        // User information variables
        $user_name = "Sarah Johnson";
        $username = "sarahj_designer";
        $bio = "UX Designer | Coffee lover | Dog mom 🐕";
        $follower_count = 1248;
        $following_count = 892;
        $post_count = 156;
        $is_verified = true;
        $is_online = true;

        // Display the profile header
        echo "<div class='profile-header'>";
        echo "<h1>" . $user_name;

        // Show verification badge if user is verified
        if ($is_verified) {
            echo " ✓";
        }
        echo "</h1>";

        echo "<p>@" . $username . "</p>";
        echo "<p>" . $bio . "</p>";
        echo "</div>";

        // Display profile statistics
        echo "<div class='profile-stats'>";

        echo "<div class='stat'>";
        echo "<div class='stat-number'>" . $post_count . "</div>";
        echo "<div class='stat-label'>Posts</div>";
        echo "</div>";

        echo "<div class='stat'>";
        echo "<div class='stat-number'>" . $follower_count . "</div>";
        echo "<div class='stat-label'>Followers</div>";
        echo "</div>";

        echo "<div class='stat'>";
        echo "<div class='stat-number'>" . $following_count . "</div>";
        echo "<div class='stat-label'>Following</div>";
        echo "</div>";

        echo "</div>";

        // Display user status
        echo "<div class='user-status' style='margin-top: 20px; padding: 15px; background: #f8f9fa; border-radius: 5px;'>";

        echo "<h3>Account Status</h3>";

        // Show online status
        if ($is_online) {
            echo "<p style='color: green;'>🟢 Currently Online</p>";
        } else {
            echo "<p style='color: gray;'>⚫ Offline</p>";
        }

        // Show verification status
        if ($is_verified) {
            echo "<p style='color: blue;'>✅ Verified Account</p>";
        } else {
            echo "<p style='color: orange;'>⚠️ Unverified Account</p>";
        }

        echo "</div>";
        ?>

        <div style="margin-top: 30px; padding-top: 20px; border-top: 1px solid #eee;">
            <h3>What You Just Built</h3>
            <p>Congratulations! You've created your first dynamic social platform page using PHP variables. This profile card demonstrates the foundation of every social network - storing and displaying user information.</p>
        </div>
    </div>
</body>
</html>
```

---

## Testing Your Work

### Quick Test Checklist:

- [ ] Page loads without errors at `http://localhost/hello-social.php`
- [ ] User name, username, and bio display correctly
- [ ] Statistics show the correct numbers
- [ ] Verification badge appears when `$is_verified` is `true`
- [ ] Online status displays correctly based on `$is_online` value

### Manual Testing:

1. **Load the page** - Open `http://localhost/hello-social.php` in your browser
2. **Verify the profile displays** - You should see Sarah Johnson's profile with all information
3. **Test variable changes** - Change `$user_name` to your own name, save, and refresh
4. **Test boolean variables** - Change `$is_verified` to `false`, save, and refresh to see the badge disappear
5. **Check for PHP errors** - If you see error messages, check that all variables end with semicolons

### Troubleshooting Common Issues:

**Problem:** "Parse error: syntax error, unexpected..." **Solution:** Check that all PHP lines end with semicolons `;` and that you have matching quote marks around strings.

**Problem:** Page shows PHP code instead of running it **Solution:** Make sure your file ends with `.php` and you're accessing it through `localhost`, not opening it directly in the browser.

**Problem:** Variables not displaying **Solution:** Verify that variable names start with `$` and are spelled consistently throughout your code.

---

## Project Progress Check

### What You've Built:

You've created your first dynamic web page that displays user profile information using PHP variables. This page demonstrates the fundamental concept behind every social platform - storing user data and displaying it dynamically.

### How It Fits:

This profile display system is the foundation for every feature we'll build:

- User registration will create this data
- The database will store this information permanently
- The timeline will show multiple users' information
- Every social feature will build on displaying user data

### What's Working Now:

- Dynamic user profile display
- Variable-based content system
- Basic social platform styling
- Status indicators for online/verification

---

## Key Takeaways

After completing this lesson, you should understand:

- PHP code runs on the server and generates HTML for browsers
- Variables store different types of information (strings, integers, booleans)
- The `echo` statement displays variables and text on web pages
- Variables make web pages dynamic by allowing content to change
- Social platforms are built on the foundation of displaying user information stored in variables

---

## Next Up

**Coming in Lesson 1.2:** Data Types for Social Platforms - User Information

**You'll learn:** How different data types handle various kinds of social platform information - from user profiles to post timestamps

**Files you'll work with:** `user-data-types.php` (exploring strings, numbers, arrays, and more)

---

## Additional Resources

### Quick References:

- [PHP Official Documentation - Variables](https://php.net/manual/en/language.variables.php)
- [PHP Echo Statement Reference](https://php.net/manual/en/function.echo.php)
- [PHP Data Types Documentation](https://php.net/manual/en/language.types.php)

### Going Deeper:

- Practice changing variable values and seeing how it affects the display
- Try adding new variables for additional profile information
- Experiment with different HTML styling in your echo statements

---

## Chapter Progress

**Lessons Completed in Chapter 1:**

- [x] Lesson 1.1: Hello Social Platform - PHP Syntax & Variables
- [ ] Lesson 1.2: Data Types for Social Platforms - User Information
- [ ] Lesson 1.3: Arrays - Storing Multiple Users and Posts
- [ ] Lesson 1.4: Loops - Displaying Dynamic Content
- [ ] Lesson 1.5: Functions - Reusable Social Platform Tools

**Chapter Goal:** Master PHP foundations while creating the basic display system for your social platform
