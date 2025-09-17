# Chapter 1, Lesson 3: Arrays - Storing Multiple Users and Posts

**Goal:** Master PHP arrays by creating a multi-user social platform displaying multiple user profiles and posts  
**Time:** 1-2 hours  
**Prerequisites:** Chapter 1, Lessons 1.1 and 1.2 completed  
**Files:** `social-feed.php`, `style.css` (updated)

---

## What You'll Learn

In this lesson, you will:

- Create indexed arrays to store lists of user information
- Build associative arrays for structured user profiles
- Construct multidimensional arrays for complex social platform data
- Access and display array data in professional layouts
- Transform your single-user profile into a multi-user social feed

---

## Why This Matters

Real social platforms don't just show one user - they display feeds of multiple users, lists of friends, collections of posts, and threads of comments. Arrays are the foundation that makes this possible. Without arrays, you'd need hundreds of individual variables to store even a small amount of social platform data.

Arrays let you organize related information together. Instead of `$user1_name`, `$user2_name`, `$user3_name`, you can have one `$users` array containing all user names. This makes your code cleaner, more manageable, and infinitely more scalable.

By mastering arrays now, you're preparing for everything that makes social platforms social - user lists, friend networks, post feeds, comment threads, and all the interconnected data that creates engaging online communities.

---

## Core Concepts

### Concept 1: Indexed Arrays - Simple Lists

**Definition:** Indexed arrays store multiple values in a single variable, accessed by numbered positions starting from 0.

**In Context:** Perfect for simple lists like usernames, post titles, or hashtags where order matters but you don't need complex structure.

**Example:**

```php
<?php
// Simple list of usernames
$usernames = ['alex_coder', 'sarah_dev', 'mike_photos', 'jessica_designs'];

// List of popular hashtags
$trending_tags = ['#coding', '#design', '#photography', '#travel'];

// Accessing array values by index (starts at 0)
echo $usernames[0]; // Shows: alex_coder
echo $usernames[1]; // Shows: sarah_dev
?>
```

**Key Points:**

- Arrays start counting at 0, not 1
- Use square brackets `[]` to create arrays
- Access items with `$array[index]`
- Great for simple, ordered lists

### Concept 2: Associative Arrays - Structured Data

**Definition:** Associative arrays use meaningful keys instead of numbers, perfect for storing structured information like user profiles.

**In Context:** Ideal for user profiles, post information, or any data where you need named properties rather than just positions.

**Example:**

```php
<?php
// User profile as associative array
$user = [
    'username' => 'sarah_dev',
    'name' => 'Sarah Johnson',
    'followers' => 1250,
    'verified' => true,
    'bio' => 'Full-stack developer who loves PHP'
];

// Accessing by meaningful keys
echo $user['name'];      // Shows: Sarah Johnson  
echo $user['followers']; // Shows: 1250
?>
```

**Key Points:**

- Use `=>` to assign keys to values
- Keys are strings (usually), values can be any data type
- More readable and self-documenting than indexed arrays
- Perfect for database-like structures

### Concept 3: Multidimensional Arrays - Complex Data

**Definition:** Arrays that contain other arrays, allowing you to store complex, nested information like multiple user profiles or posts with comments.

**In Context:** Essential for social platforms where you need to store multiple users, each with their own detailed information, or posts with associated data.

**Example:**

```php
<?php
// Array of multiple user profiles
$users = [
    [
        'username' => 'alex_coder',
        'name' => 'Alex Rivera',
        'followers' => 892,
        'posts' => 47
    ],
    [
        'username' => 'sarah_dev', 
        'name' => 'Sarah Johnson',
        'followers' => 1250,
        'posts' => 63
    ]
];

// Accessing nested data
echo $users[0]['name'];      // Shows: Alex Rivera
echo $users[1]['followers']; // Shows: 1250
?>
```

**Key Points:**

- Arrays within arrays create complex data structures
- Use multiple brackets to access nested data: `$array[0]['key']`
- Perfect for storing multiple related records
- Foundation for database-like operations

---

## Building It Step-by-Step

### Step 1: Create a Multi-User Social Feed

**What we're doing:** Building a social platform feed that displays multiple users and their posts using different types of arrays.

**The Code:**

Create a file named `social-feed.php`:

```php
<?php
/**
 * Social Platform Project - Chapter 1, Lesson 3
 * Multi-user social feed demonstrating arrays in social platform context
 */

// Simple indexed array for trending hashtags
$trending_hashtags = [
    '#WebDevelopment', '#PHP', '#JavaScript', '#Design', '#Photography', 
    '#Travel', '#Food', '#Fitness', '#Music', '#Art'
];

// Array of featured usernames
$featured_users = ['alex_coder', 'sarah_dev', 'mike_photos', 'jessica_designs', 'tom_writer'];

// Multidimensional array of user profiles
$users = [
    [
        'id' => 1,
        'username' => 'alex_coder',
        'name' => 'Alex Rivera',
        'bio' => 'Full-stack developer passionate about clean code and user experience',
        'followers' => 892,
        'following' => 245,
        'posts' => 47,
        'verified' => true,
        'avatar' => '👨‍💻',
        'join_date' => '2023-03-15',
        'is_online' => true
    ],
    [
        'id' => 2,
        'username' => 'sarah_dev',
        'name' => 'Sarah Johnson', 
        'bio' => 'Backend developer who loves PHP and building scalable systems',
        'followers' => 1250,
        'following' => 189,
        'posts' => 63,
        'verified' => true,
        'avatar' => '👩‍💻',
        'join_date' => '2022-11-08',
        'is_online' => false
    ],
    [
        'id' => 3,
        'username' => 'mike_photos',
        'name' => 'Mike Chen',
        'bio' => 'Travel photographer capturing moments around the world 📸',
        'followers' => 3420,
        'following' => 567,
        'posts' => 128,
        'verified' => true,
        'avatar' => '📸',
        'join_date' => '2021-09-22',
        'is_online' => true
    ],
    [
        'id' => 4,
        'username' => 'jessica_designs',
        'name' => 'Jessica Wong',
        'bio' => 'UX/UI Designer creating beautiful and functional user experiences',
        'followers' => 2847,
        'following' => 432,
        'posts' => 156,
        'verified' => false,
        'avatar' => '🎨',
        'join_date' => '2022-05-14',
        'is_online' => true
    ],
    [
        'id' => 5,
        'username' => 'tom_writer',
        'name' => 'Tom Anderson',
        'bio' => 'Tech writer and blogger sharing insights about the digital world',
        'followers' => 567,
        'following' => 123,
        'posts' => 89,
        'verified' => false,
        'avatar' => '✍️',
        'join_date' => '2023-01-10',
        'is_online' => false
    ]
];

// Multidimensional array of recent posts
$recent_posts = [
    [
        'id' => 101,
        'user_id' => 1,
        'username' => 'alex_coder',
        'user_name' => 'Alex Rivera',
        'content' => 'Just deployed my latest PHP project! The new features are working perfectly. Love how clean the code turned out. 🚀',
        'timestamp' => '2024-01-15 14:30:00',
        'likes' => 23,
        'comments' => 7,
        'hashtags' => ['#PHP', '#WebDevelopment', '#Coding']
    ],
    [
        'id' => 102,
        'user_id' => 3,
        'username' => 'mike_photos',
        'user_name' => 'Mike Chen',
        'content' => 'Incredible sunset from yesterday\'s hike in the mountains. Nature never fails to amaze me! 🌄',
        'timestamp' => '2024-01-15 12:45:00',
        'likes' => 156,
        'comments' => 24,
        'hashtags' => ['#Photography', '#Travel', '#Nature']
    ],
    [
        'id' => 103,
        'user_id' => 4,
        'username' => 'jessica_designs',
        'user_name' => 'Jessica Wong',
        'content' => 'Working on a new mobile app design. The user research phase revealed some fascinating insights about user behavior!',
        'timestamp' => '2024-01-15 10:20:00',
        'likes' => 89,
        'comments' => 12,
        'hashtags' => ['#Design', '#UX', '#MobileApp']
    ],
    [
        'id' => 104,
        'user_id' => 2,
        'username' => 'sarah_dev',
        'user_name' => 'Sarah Johnson',
        'content' => 'Database optimization can be tricky, but when you get it right, the performance improvements are incredible! 💪',
        'timestamp' => '2024-01-15 09:15:00',
        'likes' => 67,
        'comments' => 15,
        'hashtags' => ['#Database', '#Performance', '#PHP']
    ],
    [
        'id' => 105,
        'user_id' => 5,
        'username' => 'tom_writer',
        'user_name' => 'Tom Anderson',
        'content' => 'Writing my next article about the evolution of web development. The changes in the last 5 years have been remarkable!',
        'timestamp' => '2024-01-15 08:00:00',
        'likes' => 34,
        'comments' => 9,
        'hashtags' => ['#Writing', '#WebDevelopment', '#Tech']
    ]
];

// Calculate some statistics from our arrays
$total_users = count($users);
$total_posts = count($recent_posts);
$total_followers = 0;
foreach ($users as $user) {
    $total_followers += $user['followers'];
}
?>
<!DOCTYPE html>
<html lang="en">

<body>
    <div class="container">
        <!-- Header with platform statistics -->
        <header class="feed-header">
            <h1>🌐 ConnectHub Social Feed</h1>
            <div class="platform-stats">
                <span class="stat"><?php echo $total_users; ?> Users</span>
                <span class="stat"><?php echo $total_posts; ?> Recent Posts</span>
                <span class="stat"><?php echo number_format($total_followers); ?> Total Followers</span>
            </div>
        </header>

        <!-- Trending hashtags section -->
        <section class="trending-section">
            <h2>🔥 Trending Now</h2>
            <div class="hashtag-list">
                <?php for ($i = 0; $i < 6; $i++): ?>
                    <span class="hashtag"><?php echo $trending_hashtags[$i]; ?></span>
                <?php endfor; ?>
            </div>
        </section>

        <!-- Featured users section -->
        <section class="featured-users">
            <h2>⭐ Featured Users</h2>
            <div class="user-grid">
                <?php foreach ($users as $user): ?>
                    <div class="user-card">
                        <div class="user-avatar"><?php echo $user['avatar']; ?></div>
                        <h3><?php echo $user['name']; ?></h3>
                        <p class="username">@<?php echo $user['username']; ?></p>

                        <!-- Show verification badge if user is verified -->
                        <?php if ($user['verified']): ?>
                            <span class="verified-badge">✓</span>
                        <?php endif; ?>

                        <!-- Online status indicator -->
                        <div class="status-indicator <?php echo $user['is_online'] ? 'online' : 'offline'; ?>">
                            <?php echo $user['is_online'] ? '🟢 Online' : '🔴 Offline'; ?>
                        </div>

                        <p class="user-bio"><?php echo $user['bio']; ?></p>

                        <div class="user-stats">
                            <span><?php echo number_format($user['followers']); ?> followers</span>
                            <span><?php echo $user['posts']; ?> posts</span>
                        </div>
                    </div>
                <?php endforeach; ?>
            </div>
        </section>

        <!-- Recent posts feed -->
        <section class="posts-feed">
            <h2>📝 Recent Posts</h2>

            <?php foreach ($recent_posts as $post): ?>
                <article class="post-card">
                    <header class="post-header">
                        <!-- Find and display user info for this post -->
                        <?php
                        // Find the user who made this post
                        $post_author = null;
                        foreach ($users as $user) {
                            if ($user['id'] === $post['user_id']) {
                                $post_author = $user;
                                break;
                            }
                        }
                        ?>

                        <div class="author-info">
                            <span class="author-avatar"><?php echo $post_author['avatar']; ?></span>
                            <div class="author-details">
                                <strong><?php echo $post['user_name']; ?></strong>
                                <span class="username">@<?php echo $post['username']; ?></span>
                                <?php if ($post_author['verified']): ?>
                                    <span class="verified-mini">✓</span>
                                <?php endif; ?>
                            </div>
                        </div>

                        <time class="post-time"><?php echo date('M j, g:i A', strtotime($post['timestamp'])); ?></time>
                    </header>

                    <main class="post-content">
                        <p><?php echo $post['content']; ?></p>

                        <!-- Display hashtags for this post -->
                        <div class="post-hashtags">
                            <?php foreach ($post['hashtags'] as $hashtag): ?>
                                <span class="post-hashtag"><?php echo $hashtag; ?></span>
                            <?php endforeach; ?>
                        </div>
                    </main>

                    <footer class="post-footer">
                        <div class="post-stats">
                            <span class="likes">❤️ <?php echo $post['likes']; ?> likes</span>
                            <span class="comments">💬 <?php echo $post['comments']; ?> comments</span>
                        </div>
                    </footer>
                </article>
            <?php endforeach; ?>
        </section>

        <!-- Array demonstration section -->
        <section class="array-demo">
            <h2>🔍 Behind the Scenes: Array Data</h2>

            <div class="demo-grid">
                <div class="demo-card">
                    <h3>Indexed Array Example</h3>
                    <p><strong>Trending Hashtags:</strong></p>
                    <code>
                        $trending_hashtags = [<br>
                          '<?php echo $trending_hashtags[0]; ?>',<br>
                          '<?php echo $trending_hashtags[1]; ?>',<br>
                          '<?php echo $trending_hashtags[2]; ?>'<br>
                        ];
                    </code>
                </div>

                <div class="demo-card">
                    <h3>Associative Array Example</h3>
                    <p><strong>First User Profile:</strong></p>
                    <code>
                        $user = [<br>
                          'name' => '<?php echo $users[0]['name']; ?>',<br>
                          'username' => '<?php echo $users[0]['username']; ?>',<br>
                          'followers' => <?php echo $users[0]['followers']; ?><br>
                        ];
                    </code>
                </div>

                <div class="demo-card">
                    <h3>Multidimensional Array</h3>
                    <p><strong>Multiple Users:</strong></p>
                    <code>
                        $users[0]['name'] = '<?php echo $users[0]['name']; ?>'<br>
                        $users[1]['name'] = '<?php echo $users[1]['name']; ?>'<br>
                        $users[2]['name'] = '<?php echo $users[2]['name']; ?>'
                    </code>
                </div>
            </div>
        </section>

        <footer class="feed-footer">
            <p>
                ConnectHub Social Feed powered by PHP Arrays | 
                Displaying <?php echo count($users); ?> users and <?php echo count($recent_posts); ?> posts |
                Generated on <?php echo date('F j, Y \a\t g:i A'); ?>
            </p>
        </footer>
    </div>
</body>
</html>
```

**Understanding the Code:**

- **Indexed Arrays:** Store simple lists like hashtags and usernames
- **Associative Arrays:** Structure user profiles with meaningful keys
- **Multidimensional Arrays:** Store multiple users and posts with complex data
- **Array Loops:** Use `foreach` to display all items in arrays
- **Array Functions:** Use `count()` to get array sizes and calculate statistics
- **Data Relationships:** Connect posts to users by matching IDs

**Testing It:** Save the file and open it in your browser. You should see a complete social feed with multiple users and posts.

### Step 2: Add CSS Styling for the Social Feed

**What we're doing:** Creating professional styling for our multi-user social feed layout.

**The Code:**

Add these styles to the end of your `style.css` file:

```css
/* Social Feed Styles - Chapter 1, Lesson 3 */

/* Feed header */
.feed-header {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    padding: 30px;
    text-align: center;
    margin-bottom: 30px;
    border-radius: 12px;
}

.feed-header h1 {
    font-size: 2.2rem;
    margin-bottom: 15px;
}

.platform-stats {
    display: flex;
    justify-content: center;
    gap: 30px;
    flex-wrap: wrap;
}

.platform-stats .stat {
    background: rgba(255, 255, 255, 0.2);
    padding: 8px 16px;
    border-radius: 20px;
    font-weight: 600;
}

/* Trending section */
.trending-section {
    margin-bottom: 30px;
    text-align: center;
}

.hashtag-list {
    display: flex;
    justify-content: center;
    gap: 10px;
    flex-wrap: wrap;
    margin-top: 15px;
}

.hashtag {
    background: #667eea;
    color: white;
    padding: 6px 12px;
    border-radius: 15px;
    font-size: 0.85rem;
    font-weight: 600;
}

/* Featured users grid */
.featured-users {
    margin-bottom: 40px;
}

.user-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
    margin-top: 20px;
}

.user-card {
    background: white;
    border: 1px solid #e1e5e9;
    border-radius: 12px;
    padding: 20px;
    text-align: center;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    transition: transform 0.2s ease;
}

.user-card:hover {
    transform: translateY(-2px);
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
}

.user-avatar {
    font-size: 3rem;
    margin-bottom: 10px;
}

.user-card h3 {
    margin-bottom: 5px;
    color: #333;
}

.user-card .username {
    color: #666;
    font-size: 0.9rem;
    margin-bottom: 10px;
}

.verified-badge {
    background: #28a745;
    color: white;
    padding: 2px 8px;
    border-radius: 10px;
    font-size: 0.7rem;
    margin-left: 5px;
}

.status-indicator {
    font-size: 0.8rem;
    margin: 10px 0;
    font-weight: 600;
}

.status-indicator.online {
    color: #28a745;
}

.status-indicator.offline {
    color: #6c757d;
}

.user-bio {
    color: #666;
    font-size: 0.9rem;
    line-height: 1.4;
    margin-bottom: 15px;
}

.user-stats {
    display: flex;
    justify-content: space-around;
    padding-top: 15px;
    border-top: 1px solid #e1e5e9;
    color: #666;
    font-size: 0.85rem;
}

/* Posts feed */
.posts-feed {
    margin-bottom: 40px;
}

.post-card {
    background: white;
    border: 1px solid #e1e5e9;
    border-radius: 12px;
    margin-bottom: 20px;
    overflow: hidden;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.post-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px 20px;
    border-bottom: 1px solid #f1f3f4;
}

.author-info {
    display: flex;
    align-items: center;
    gap: 12px;
}

.author-avatar {
    font-size: 1.8rem;
}

.author-details strong {
    display: block;
    color: #333;
}

.author-details .username {
    font-size: 0.85rem;
    color: #666;
}

.verified-mini {
    color: #28a745;
    font-size: 0.8rem;
    margin-left: 5px;
}

.post-time {
    color: #666;
    font-size: 0.85rem;
}

.post-content {
    padding: 0 20px 15px;
}

.post-content p {
    color: #333;
    line-height: 1.6;
    margin-bottom: 15px;
}

.post-hashtags {
    display: flex;
    gap: 8px;
    flex-wrap: wrap;
}

.post-hashtag {
    background: #f8f9fa;
    color: #667eea;
    padding: 4px 8px;
    border-radius: 8px;
    font-size: 0.8rem;
    font-weight: 600;
}

.post-footer {
    padding: 15px 20px;
    border-top: 1px solid #f1f3f4;
    background: #fafbfc;
}

.post-stats {
    display: flex;
    gap: 20px;
    color: #666;
    font-size: 0.9rem;
}

/* Array demonstration */
.array-demo {
    background: #f8f9fa;
    padding: 30px;
    border-radius: 12px;
    margin-bottom: 30px;
}

.demo-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 20px;
    margin-top: 20px;
}

.demo-card {
    background: white;
    padding: 20px;
    border-radius: 8px;
    border-left: 4px solid #667eea;
}

.demo-card h3 {
    color: #333;
    margin-bottom: 10px;
}

.demo-card code {
    display: block;
    background: #f1f3f4;
    padding: 15px;
    border-radius: 6px;
    font-family: 'Courier New', monospace;
    font-size: 0.85rem;
    color: #333;
    margin-top: 10px;
    line-height: 1.4;
}

/* Responsive design */
@media (max-width: 768px) {
    .platform-stats {
        flex-direction: column;
        gap: 10px;
    }

    .hashtag-list {
        justify-content: flex-start;
    }

    .user-grid {
        grid-template-columns: 1fr;
    }

    .post-header {
        flex-direction: column;
        align-items: flex-start;
        gap: 10px;
    }

    .demo-grid {
        grid-template-columns: 1fr;
    }
}
```

---

## Testing Your Work

### Quick Test Checklist:

- [ ] Multiple users display in grid layout
- [ ] All user information shows correctly from arrays
- [ ] Posts display with correct author information
- [ ] Hashtags appear for each post
- [ ] Online/offline status shows correctly
- [ ] Verification badges appear for verified users
- [ ] Array demonstration section shows code examples
- [ ] Platform statistics calculate correctly

### Manual Testing:

1. **Array Access:** Verify that user names, usernames, and stats display correctly
2. **Loops:** Check that all 5 users and all 5 posts appear
3. **Data Relationships:** Confirm posts show correct author information
4. **Array Calculations:** Verify total followers count is accurate
5. **Mobile View:** Resize browser to test responsive design

### Troubleshooting Common Issues:

**Problem:** "Undefined index" error when accessing array elements  
**Solution:** Make sure array keys are spelled correctly and exist: `$user['username']` not `$user['user_name']`

**Problem:** Posts show wrong author information  
**Solution:** Check that user IDs in posts match user IDs in the users array

**Problem:** Only some users/posts display  
**Solution:** Verify `foreach` loops are properly structured and arrays contain expected data

---

## Project Progress Check

### What You've Built:

You've transformed your single-user profile into a complete multi-user social platform feed. The system now displays multiple users with their profiles, shows recent posts from different users, and demonstrates how arrays organize complex social platform data.

### How It Fits:

This multi-user feed represents the core of any social platform - the ability to display content from multiple users in an organized, engaging format. You've built the foundation for user discovery, content feeds, and social interactions.

### What's Working Now:

- Multi-user profile display system
- Social media post feed with author information
- Trending hashtags and user discovery
- Complex data relationships between users and posts
- Professional responsive layout for all screen sizes
- Live demonstration of array concepts in action

---

## Key Takeaways

After completing this lesson, you should understand:

- **Indexed arrays** store simple lists accessed by numbered positions
- **Associative arrays** use meaningful keys to organize structured data
- **Multidimensional arrays** handle complex, nested information like multiple user profiles
- **Array loops** with `foreach` efficiently display all array contents
- **Data relationships** can be created by matching IDs between different arrays

---

## Next Up

**Coming in Lesson 1.4:** Loops - Displaying Dynamic Content

**You'll learn:** Different types of PHP loops (`for`, `while`, `foreach`) and how to use them to efficiently display social platform content, handle user interactions, and process large amounts of data.

**Files you'll work with:** You'll enhance `social-feed.php` with advanced looping techniques for pagination, content filtering, and dynamic displays.

---

## Chapter Progress

**Lessons Completed in Chapter 1:**

- [x] Lesson 1.1: Hello Social Platform - PHP Syntax & Variables
- [x] Lesson 1.2: Data Types for Social Platforms - User Information
- [x] Lesson 1.3: Arrays - Storing Multiple Users and Posts
- [ ] Lesson 1.4: Loops - Displaying Dynamic Content
- [ ] Lesson 1.5: Functions - Reusable Social Platform Tools

**Chapter Goal:** Master PHP basics while creating dynamic content for our social platform foundation.
