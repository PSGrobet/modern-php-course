# Chapter 1, Lesson 2: Data Types for Social Platforms - User Information

**Goal:** Master PHP data types by creating a comprehensive user profile with different kinds of social platform information  
**Time:** 1-2 hours  
**Prerequisites:** Chapter 1, Lesson 1 completed  
**Files:** `user-data-types.php`, `style.css` (updated)

---

## What You'll Learn

In this lesson, you will:

- Understand the four main PHP data types used in social platforms
- Work with strings for user names, bios, and post content
- Use integers and floats for counts, ratings, and measurements
- Apply boolean values for user settings and status flags
- Create more sophisticated user profiles with mixed data types

---

## Why This Matters

Real social platforms handle incredibly diverse types of information. A single user profile might contain text (name, bio), numbers (follower count, age), true/false values (verification status, privacy settings), and much more. Understanding PHP data types is crucial because different types of data behave differently and have different capabilities.

For example, you can do math with numbers but not with text. You can check if a boolean is true or false, but that doesn't make sense for a username. When we start connecting to databases later in the course, understanding data types becomes even more important for storing and retrieving information efficiently.

By mastering data types now, you're building the foundation for handling user registrations, post creation, comment systems, and all the complex data that makes social platforms work.

---

## Core Concepts

### Concept 1: Strings - Text Information

**Definition:** Strings hold text data like usernames, bios, post content, and any other textual information users might enter.

**In Context:** Almost everything users see on social platforms starts as string data - usernames, post content, comments, bio text, location names, and more.

**Example:**

```php
<?php
// Single quotes for simple text
$username = 'sarah_dev';
$location = 'San Francisco';

// Double quotes when you need special characters or variables
$bio = "I'm a developer who loves PHP and building cool stuff!";
$welcome_message = "Welcome back, $username!";

// Multiline strings for longer content
$post_content = "Just finished building my first social platform feature! 
It's amazing how much you can do with PHP. 
Can't wait to add more functionality! 🚀";
?>
```

**Key Points:**

- Use single quotes (`'`) for simple text that won't change
- Use double quotes (`"`) when you need variables inside the string
- Strings can be any length and contain any characters
- Use escape characters (`\'`) for quotes within quotes

### Concept 2: Integers - Counting and Whole Numbers

**Definition:** Integers are whole numbers (no decimals) used for counting things like followers, posts, likes, and ages.

**In Context:** Social platforms are full of counts - how many followers someone has, how many posts they've made, how many likes a photo got, what year they joined.

**Example:**

```php
<?php
// User statistics
$followers = 1250;
$following = 890;
$posts = 47;
$likes_received = 15680;

// User information
$age = 28;
$join_year = 2021;
$login_streak = 15; // days in a row

// You can do math with integers
$total_connections = $followers + $following;
$years_active = 2024 - $join_year;
?>
```

**Key Points:**

- No decimal points (use floats for those)
- Can be positive, negative, or zero
- Perfect for counting and mathematical operations
- PHP handles large numbers automatically

### Concept 3: Floats - Numbers with Decimals

**Definition:** Float numbers (also called "floating-point" or "double") include decimal points and are used for ratings, percentages, and precise measurements.

**In Context:** Social platforms use floats for user ratings, engagement percentages, average post performance, and any measurement that needs precision.

**Example:**

```php
<?php
// User engagement metrics
$average_likes_per_post = 234.7;
$engagement_rate = 4.23; // percentage
$profile_completion = 87.5; // percentage

// Rating systems
$user_rating = 4.8; // out of 5 stars
$content_quality_score = 9.2; // out of 10

// Time-based measurements
$average_session_time = 23.5; // minutes
?>
```

**Key Points:**

- Include decimal points for precision
- Great for averages, percentages, and ratings
- Can represent very large or very small numbers
- Useful for calculations that don't result in whole numbers

### Concept 4: Booleans - True/False Settings

**Definition:** Boolean values are either `true` or `false`, perfect for settings, status flags, and yes/no questions.

**In Context:** Social platforms have many on/off settings - is a user verified? Is their profile private? Are notifications enabled? Has a post been liked by the current user?

**Example:**

```php
<?php
// User account status
$is_verified = true;
$is_private = false;
$is_online = true;
$is_banned = false;

// User preferences
$email_notifications = true;
$dark_mode = false;
$show_phone = false;
$allow_messages = true;

// Post status
$is_published = true;
$allows_comments = true;
$is_pinned = false;
?>
```

**Key Points:**

- Only two possible values: `true` or `false`
- Perfect for settings and yes/no questions
- Used extensively in conditional statements (`if/else`)
- Automatically convert to 1 (true) or 0 (false) when needed

---

## Building It Step-by-Step

### Step 1: Create a Comprehensive User Profile

**What we're doing:** Building a detailed user profile that demonstrates all four data types working together in a realistic social platform context.

**The Code:**

Create a file named `user-data-types.php`:

```php
<?php
/**
 * Social Platform Project - Chapter 1, Lesson 2
 * Demonstrating different data types through a comprehensive user profile
 */

// STRING DATA - Text information about the user
$username = 'jessica_designs';
$display_name = 'Jessica Chen';
$first_name = 'Jessica';
$last_name = 'Chen';
$bio = "UX/UI Designer passionate about creating beautiful, user-friendly experiences. Always learning something new! 🎨";
$location = 'Seattle, WA';
$website = 'https://jessicachen.design';
$job_title = 'Senior UX Designer';
$company = 'TechFlow Studios';

// More complex string data
$favorite_quote = "Design is not just what it looks like and feels like. Design is how it works. - Steve Jobs";
$recent_post = "Just wrapped up an amazing design sprint! Our team created three different prototypes for the new mobile app. Collaboration at its finest! 💪 #design #teamwork";

// INTEGER DATA - Whole numbers for counting
$followers = 2847;
$following = 1205;
$posts = 156;
$likes_received = 38920;
$comments_made = 892;
$age = 29;
$join_year = 2020;
$profile_views = 5643;
$login_streak = 28; // consecutive days

// FLOAT DATA - Numbers with decimals for precise measurements
$average_likes_per_post = 249.6;
$engagement_rate = 7.82; // percentage
$profile_completion = 94.5; // percentage
$user_rating = 4.9; // out of 5 stars from collaborators
$average_response_time = 2.3; // hours for messages
$content_quality_score = 8.7; // out of 10

// BOOLEAN DATA - True/false settings and status
$is_verified = true;
$is_private = false;
$is_online = true;
$is_premium = true;
$is_banned = false;

// User preferences (booleans)
$email_notifications = true;
$push_notifications = false;
$dark_mode = true;
$show_email = false;
$show_phone = false;
$allow_messages_from_strangers = false;
$show_activity_status = true;

// Post and content settings
$allow_comments_on_posts = true;
$allow_post_sharing = true;
$watermark_images = true;

// Calculate some derived values using different data types
$total_interactions = $likes_received + $comments_made; // integer math
$years_active = 2024 - $join_year; // integer calculation
$likes_per_follower = round($likes_received / $followers, 2); // float calculation
$is_power_user = ($followers > 1000 && $posts > 100); // boolean logic
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
        <!-- Profile Header Section -->
        <header class="profile-header">
            <div class="header-content">
                <h1><?php echo $display_name; ?></h1>
                <p class="username">@<?php echo $username; ?></p>

                <!-- Boolean data controls what badges show -->
                <div class="badges">
                    <?php if ($is_verified): ?>
                        <span class="badge verified">✓ Verified</span>
                    <?php endif; ?>

                    <?php if ($is_premium): ?>
                        <span class="badge premium">⭐ Premium</span>
                    <?php endif; ?>

                    <?php if ($is_power_user): ?>
                        <span class="badge power-user">🚀 Power User</span>
                    <?php endif; ?>

                    <!-- Online status using boolean -->
                    <span class="status-indicator <?php echo $is_online ? 'online' : 'offline'; ?>">
                        <?php echo $is_online ? 'Online' : 'Offline'; ?>
                    </span>
                </div>
            </div>
        </header>

        <!-- Personal Information Section -->
        <main class="profile-content">
            <section class="personal-info">
                <h2>About <?php echo $first_name; ?></h2>

                <!-- String data display -->
                <div class="info-grid">
                    <div class="info-item">
                        <strong>Bio:</strong>
                        <p><?php echo $bio; ?></p>
                    </div>

                    <div class="info-item">
                        <strong>Location:</strong>
                        <span><?php echo $location; ?></span>
                    </div>

                    <div class="info-item">
                        <strong>Job:</strong>
                        <span><?php echo $job_title; ?> at <?php echo $company; ?></span>
                    </div>

                    <div class="info-item">
                        <strong>Website:</strong>
                        <a href="<?php echo $website; ?>" target="_blank"><?php echo $website; ?></a>
                    </div>

                    <!-- Integer data display -->
                    <div class="info-item">
                        <strong>Age:</strong>
                        <span><?php echo $age; ?> years old</span>
                    </div>

                    <div class="info-item">
                        <strong>Member Since:</strong>
                        <span><?php echo $join_year; ?> (<?php echo $years_active; ?> years active)</span>
                    </div>
                </div>
            </section>

            <!-- Statistics Section - Mixing integers and floats -->
            <section class="statistics">
                <h2>Profile Statistics</h2>

                <div class="stats-grid">
                    <!-- Basic counts (integers) -->
                    <div class="stat-card">
                        <h3><?php echo number_format($followers); ?></h3>
                        <p>Followers</p>
                    </div>

                    <div class="stat-card">
                        <h3><?php echo number_format($following); ?></h3>
                        <p>Following</p>
                    </div>

                    <div class="stat-card">
                        <h3><?php echo $posts; ?></h3>
                        <p>Posts</p>
                    </div>

                    <div class="stat-card">
                        <h3><?php echo number_format($likes_received); ?></h3>
                        <p>Likes Received</p>
                    </div>
                </div>

                <!-- Advanced metrics (floats) -->
                <div class="advanced-stats">
                    <h3>Engagement Metrics</h3>

                    <div class="metric">
                        <span>Average likes per post:</span>
                        <strong><?php echo $average_likes_per_post; ?></strong>
                    </div>

                    <div class="metric">
                        <span>Engagement rate:</span>
                        <strong><?php echo $engagement_rate; ?>%</strong>
                    </div>

                    <div class="metric">
                        <span>Profile completion:</span>
                        <strong><?php echo $profile_completion; ?>%</strong>
                    </div>

                    <div class="metric">
                        <span>User rating:</span>
                        <strong><?php echo $user_rating; ?>/5.0 ⭐</strong>
                    </div>

                    <div class="metric">
                        <span>Likes per follower:</span>
                        <strong><?php echo $likes_per_follower; ?></strong>
                    </div>
                </div>
            </section>

            <!-- Privacy Settings Section - Boolean showcase -->
            <section class="privacy-settings">
                <h2>Account Settings</h2>

                <div class="settings-grid">
                    <div class="setting-item">
                        <span>Profile Privacy:</span>
                        <strong><?php echo $is_private ? 'Private' : 'Public'; ?></strong>
                    </div>

                    <div class="setting-item">
                        <span>Email Notifications:</span>
                        <strong><?php echo $email_notifications ? 'Enabled' : 'Disabled'; ?></strong>
                    </div>

                    <div class="setting-item">
                        <span>Push Notifications:</span>
                        <strong><?php echo $push_notifications ? 'Enabled' : 'Disabled'; ?></strong>
                    </div>

                    <div class="setting-item">
                        <span>Dark Mode:</span>
                        <strong><?php echo $dark_mode ? 'On' : 'Off'; ?></strong>
                    </div>

                    <div class="setting-item">
                        <span>Show Email:</span>
                        <strong><?php echo $show_email ? 'Public' : 'Hidden'; ?></strong>
                    </div>

                    <div class="setting-item">
                        <span>Allow Messages from Strangers:</span>
                        <strong><?php echo $allow_messages_from_strangers ? 'Yes' : 'No'; ?></strong>
                    </div>
                </div>
            </section>

            <!-- Recent Activity - String content -->
            <section class="recent-activity">
                <h2>Recent Activity</h2>

                <div class="activity-item">
                    <h4>Latest Post</h4>
                    <p><?php echo $recent_post; ?></p>
                    <small>Posted <?php echo $login_streak; ?> days ago</small>
                </div>

                <div class="activity-item">
                    <h4>Favorite Quote</h4>
                    <blockquote><?php echo $favorite_quote; ?></blockquote>
                </div>

                <!-- Dynamic message using all data types -->
                <div class="activity-item">
                    <h4>Profile Summary</h4>
                    <p>
                        <?php 
                        echo $display_name . " is a " . $age . "-year-old " . $job_title . " from " . $location . ". ";
                        echo "With " . number_format($followers) . " followers and an engagement rate of " . $engagement_rate . "%, ";
                        echo $first_name . " is definitely making an impact! ";

                        if ($is_verified && $is_premium) {
                            echo "As a verified premium member, they have access to all platform features.";
                        } elseif ($is_verified) {
                            echo "Their verified status shows they're a trusted member of our community.";
                        } else {
                            echo "They're building their reputation in our community.";
                        }
                        ?>
                    </p>
                </div>
            </section>
        </main>

        <footer class="profile-footer">
            <p>
                Profile data types: 
                <span class="data-type">Strings</span>, 
                <span class="data-type">Integers</span>, 
                <span class="data-type">Floats</span>, 
                <span class="data-type">Booleans</span> | 
                Generated on <?php echo date('F j, Y \a\t g:i A'); ?>
            </p>
        </footer>
    </div>
</body>
</html>
```

**Understanding the Code:**

- **String Variables:** We store all text data like names, bio, location, and post content
- **Integer Variables:** We use whole numbers for counts, ages, and years
- **Float Variables:** We include decimal numbers for rates, percentages, and averages
- **Boolean Variables:** We set true/false values for settings and status flags
- **Mixed Calculations:** We combine different data types to create derived values
- **Conditional Display:** We use boolean values to show/hide different content sections

**Testing It:** Save the file and open it in your browser. You should see a comprehensive profile page showcasing all four data types in realistic social platform contexts.

### Step 2: Update CSS for Enhanced Styling

**What we're doing:** Adding new styles for our expanded profile layout and data type demonstrations.

**The Code:**

Update your `style.css` file by adding these new styles at the end:

```css
/* Additional styles for Lesson 1.2 - Data Types */

/* Enhanced header with badges */
.header-content {
    text-align: center;
}

.badges {
    margin-top: 15px;
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    gap: 10px;
}

.badge {
    padding: 4px 12px;
    border-radius: 20px;
    font-size: 0.8rem;
    font-weight: 600;
}

.badge.verified {
    background: #28a745;
    color: white;
}

.badge.premium {
    background: #ffc107;
    color: #212529;
}

.badge.power-user {
    background: #6f42c1;
    color: white;
}

.status-indicator {
    padding: 4px 12px;
    border-radius: 20px;
    font-size: 0.8rem;
    font-weight: 600;
}

.status-indicator.online {
    background: #d4edda;
    color: #155724;
}

.status-indicator.offline {
    background: #f8d7da;
    color: #721c24;
}

/* Personal information section */
.personal-info {
    margin-bottom: 30px;
}

.info-grid {
    display: grid;
    gap: 15px;
    margin-top: 20px;
}

.info-item {
    padding: 15px;
    background: #f8f9fa;
    border-radius: 8px;
    border-left: 4px solid #667eea;
}

.info-item strong {
    display: block;
    color: #333;
    margin-bottom: 5px;
}

.info-item p, .info-item span {
    color: #666;
    margin: 0;
}

.info-item a {
    color: #667eea;
    text-decoration: none;
}

.info-item a:hover {
    text-decoration: underline;
}

/* Statistics section */
.statistics {
    margin-bottom: 30px;
}

.stats-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    gap: 20px;
    margin: 20px 0;
}

.stat-card {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    padding: 20px;
    border-radius: 12px;
    text-align: center;
}

.stat-card h3 {
    font-size: 2rem;
    margin: 0 0 10px 0;
    font-weight: 700;
}

.stat-card p {
    margin: 0;
    font-size: 0.9rem;
    opacity: 0.9;
}

/* Advanced stats */
.advanced-stats {
    background: #f8f9fa;
    padding: 20px;
    border-radius: 8px;
    margin-top: 20px;
}

.advanced-stats h3 {
    margin-bottom: 15px;
    color: #333;
}

.metric {
    display: flex;
    justify-content: space-between;
    padding: 10px 0;
    border-bottom: 1px solid #e9ecef;
}

.metric:last-child {
    border-bottom: none;
}

.metric span {
    color: #666;
}

.metric strong {
    color: #333;
}

/* Privacy settings section */
.privacy-settings {
    margin-bottom: 30px;
}

.settings-grid {
    display: grid;
    gap: 10px;
    margin-top: 20px;
}

.setting-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 12px 15px;
    background: #ffffff;
    border: 1px solid #e9ecef;
    border-radius: 6px;
}

.setting-item span {
    color: #666;
}

.setting-item strong {
    color: #333;
    font-weight: 600;
}

/* Recent activity section */
.recent-activity {
    margin-bottom: 20px;
}

.activity-item {
    background: #ffffff;
    border: 1px solid #e9ecef;
    border-radius: 8px;
    padding: 20px;
    margin-bottom: 15px;
}

.activity-item h4 {
    color: #333;
    margin-bottom: 10px;
}

.activity-item p {
    color: #666;
    line-height: 1.6;
    margin-bottom: 10px;
}

.activity-item blockquote {
    font-style: italic;
    color: #555;
    border-left: 4px solid #667eea;
    padding-left: 15px;
    margin: 0;
}

.activity-item small {
    color: #888;
    font-size: 0.8rem;
}

/* Footer enhancement */
.data-type {
    background: #667eea;
    color: white;
    padding: 2px 8px;
    border-radius: 12px;
    font-size: 0.7rem;
    font-weight: 600;
}

/* Responsive improvements */
@media (max-width: 768px) {
    .badges {
        flex-direction: column;
        align-items: center;
    }

    .stats-grid {
        grid-template-columns: repeat(2, 1fr);
    }

    .metric {
        flex-direction: column;
        align-items: flex-start;
        gap: 5px;
    }

    .setting-item {
        flex-direction: column;
        align-items: flex-start;
        gap: 5px;
    }
}
```

**Understanding the CSS:**

- **Badge System:** Visual indicators for different user statuses using boolean values
- **Grid Layouts:** Responsive grids for statistics and settings
- **Data Type Visualization:** Different styling for different types of content
- **Interactive Elements:** Hover effects and visual feedback
- **Mobile Optimization:** Responsive design that works on all screen sizes

**Testing It:** Refresh your browser to see the enhanced styling applied to your comprehensive user profile.

---

## Complete Code Files

### user-data-types.php

[Complete file code as shown in Step 1 above - same content]

---

## Testing Your Work

### Quick Test Checklist:

- [ ] All four data types are clearly demonstrated
- [ ] User profile displays comprehensive information
- [ ] Boolean values control badge and status display
- [ ] Integer calculations show correctly (years active, total interactions)
- [ ] Float values display with proper decimal places
- [ ] Settings section shows true/false values as readable text
- [ ] Mixed data types work together in summary paragraph
- [ ] CSS styling makes different sections clearly distinguishable

### Manual Testing:

1. **Test Boolean Logic:** Change `$is_verified` to `false` and refresh - verify badge disappears
2. **Test Integer Math:** Modify follower/following numbers and check total connections
3. **Test Float Precision:** Change engagement rate and verify decimal display
4. **Test String Concatenation:** Modify name components and check dynamic messages
5. **Test Conditional Display:** Toggle various boolean settings and observe changes

### Troubleshooting Common Issues:

**Problem:** Numbers appear without proper formatting (like 1250000 instead of 1,250,000)  
**Solution:** Use `number_format()` function for large numbers: `<?php echo number_format($followers); ?>`

**Problem:** Boolean values show as 1 or 0 instead of "Yes/No" or "Enabled/Disabled"  
**Solution:** Use ternary operators: `<?php echo $setting ? 'Enabled' : 'Disabled'; ?>`

**Problem:** Float calculations show too many decimal places  
**Solution:** Use `round()` function: `<?php echo round($likes_per_follower, 2); ?>`

---

## Project Progress Check

### What You've Built:

You've created a sophisticated user profile system that demonstrates all four major PHP data types in realistic social platform scenarios. The profile includes personal information, statistics, settings, and dynamic content that changes based on the data.

### How It Fits:

This comprehensive profile system shows how different data types work together in real applications. You've built the foundation for handling user information, preferences, statistics, and content - all essential components of any social platform.

### What's Working Now:

- Complete user profile with mixed data types
- Dynamic badge system based on boolean values
- Statistical calculations using integers and floats
- Privacy settings management with boolean toggles
- Professional styling that accommodates different content types
- Responsive design that works across devices

---

## Key Takeaways

After completing this lesson, you should understand:

- **Strings** hold text data and can be concatenated and displayed in various ways
- **Integers** are perfect for counting and mathematical operations without decimals
- **Floats** provide precision for percentages, ratings, and calculated values
- **Booleans** control conditional display and represent yes/no, on/off settings
- **Data Type Mixing** allows different types to work together in calculations and displays

---

## Next Up

**Coming in Lesson 1.3:** Arrays - Storing Multiple Users and Posts

**You'll learn:** How to use arrays to store collections of data like friend lists, post feeds, comment threads, and user groups - taking your social platform from single-user to multi-user functionality.

**Files you'll work with:** You'll create `user-arrays.php` to demonstrate how arrays store multiple users, posts, and social interactions.

---

## Additional Resources

### Quick References:

- [PHP Data Types Documentation](https://www.php.net/manual/en/language.types.php)
- [PHP String Functions](https://www.php.net/manual/en/ref.strings.php)
- [PHP Math Functions](https://www.php.net/manual/en/ref.math.php)

### Going Deeper:

- Type casting and conversion between data types
- String manipulation functions for user-generated content
- Number formatting for international applications

---

## Chapter Progress

**Lessons Completed in Chapter 1:**

- [x] Lesson 1.1: Hello Social Platform - PHP Syntax & Variables
- [x] Lesson 1.2: Data Types for Social Platforms - User Information
- [ ] Lesson 1.3: Arrays - Storing Multiple Users and Posts
- [ ] Lesson 1.4: Loops - Displaying Dynamic Content
- [ ] Lesson 1.5: Functions - Reusable Social Platform Tools

**Chapter Goal:** Master PHP basics while creating dynamic content for our social platform foundation.
