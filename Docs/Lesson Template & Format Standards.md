# Lesson Template & Format Standards

## Standard Lesson Template

**Key Constraints:**

- **100 lines of new code maximum per lesson** (excluding shared CSS)
- **One CSS file per chapter** (styles.css) - shared across all lessons
- **Focus on PHP functionality** - minimal design complexity
- **Dark theme with reusable classes**

---

# Chapter X, Lesson X.X: [Descriptive Title]

**Goal:** [One clear sentence describing what students will achieve]  
**Time:** 1-2 hours  
**Prerequisites:** [Previous lesson or specific knowledge]  
**New Code:** ~100 lines PHP/HTML

---

## What You'll Build

In this lesson, you will:

- [Specific functionality 1]
- [Specific functionality 2]
- [Specific functionality 3]

---

## Why This Matters

[1-2 paragraphs explaining the PHP concepts and their practical application to social platforms]

---

## Core Concept: [Main PHP Topic]

**Definition:** [Clear explanation of the PHP concept]

**Syntax:**

```php
// Focused code example showing the concept
$example = "Clear, practical demonstration";
```

**In Our Platform:** [How this applies to the social platform feature]

---

## Step-by-Step Implementation

### Step 1: [Descriptive Action]

**What we're doing:** [Brief purpose explanation]

```php
<?php
/**
 * Social Platform - Chapter X, Lesson X.X
 * [File purpose]
 */

// New code for this step (10-20 lines)
// Clear comments explaining PHP-specific parts
?>
```

**Key PHP Points:**

- [Important concept 1]
- [Important concept 2]

### Step 2: [Next Action]

[Continue same format - keep each step focused and small]

### Step 3: [Final Integration]

[Show how pieces connect]

---

## Complete Code

### filename.php

```php
<?php
/**
 * Social Platform - Chapter X, Lesson X.X  
 * [Complete file description]
 */

// Complete, working code (max 100 lines)
// Every line commented for learning
// Includes error handling and security basics
?>
```

---

## Testing Your Work

### Quick Verification:

1. [Specific test step 1]
2. [Specific test step 2]
3. [Expected result]

### Troubleshooting:

**Issue:** [Common problem]  
**Fix:** [Clear solution]

**Issue:** [Another common problem]  
**Fix:** [Clear solution]

---

## What You've Accomplished

✅ [Specific feature now working]  
✅ [PHP concept mastered]  
✅ [Integration completed]

**Your platform can now:** [New capability description]

---

## Next Up

**Lesson X.X:** [Next lesson title and main feature]

---

## Code Guidelines

### PHP Style Standards

```php
<?php
// File header with purpose
/**
 * Social Platform - Chapter X, Lesson X.X
 * [Brief file description]
 */

// Clear variable names
$user_posts = [];           // Good
$up = [];                   // Bad

// Consistent spacing and indentation (4 spaces)
if ($user_logged_in) {
    echo "Welcome back!";

    if ($has_notifications) {
        show_notifications();
    }
}

// Always include basic error handling
try {
    $stmt = $pdo->prepare($sql);
    $stmt->execute($params);
} catch (PDOException $e) {
    error_log($e->getMessage());
    die("Database error occurred");
}
?>
```

### HTML Integration

```php
<!-- PHP within HTML for larger content blocks -->
<article class="post-card">
    <header class="post-header">
        <h3><?php echo htmlspecialchars($post['title']); ?></h3>
        <span class="post-meta">
            By <?php echo htmlspecialchars($post['username']); ?>
            on <?php echo date('M j, Y', strtotime($post['created_at'])); ?>
        </span>
    </header>
    <div class="post-content">
        <?php echo nl2br(htmlspecialchars($post['content'])); ?>
    </div>
</article>
```

---

## CSS Standards (Chapter-Level)

### Dark Theme Base Classes

```css
/* Chapter X styles.css - Shared across all lessons */

/* Layout */
.container { max-width: 800px; margin: 0 auto; padding: 20px; }
.card { background: #2a2a2a; padding: 20px; margin: 15px 0; border-radius: 5px; }
.flex { display: flex; align-items: center; gap: 10px; }

/* Typography */
body { background: #1a1a1a; color: #ccc; font-family: Arial, sans-serif; }
.title { color: #fff; font-size: 1.4rem; margin-bottom: 10px; }
.text { color: #ccc; line-height: 1.5; }
.muted { color: #888; font-size: 0.9rem; }

/* Forms */
.form-group { margin-bottom: 15px; }
.input { width: 100%; padding: 10px; background: #333; color: #fff; border: 1px solid #555; }
.btn { padding: 10px 20px; background: #444; color: #fff; border: none; cursor: pointer; }
.btn-primary { background: #007acc; }

/* Components */
.post-card { background: #2a2a2a; padding: 15px; margin: 10px 0; }
.user-avatar { width: 40px; height: 40px; border-radius: 50%; }
.nav-link { color: #ccc; text-decoration: none; padding: 10px; }
.nav-link:hover { color: #fff; }
```

---

## Section-Specific Adaptations

### Section 1: Learning Focus

#### Comment Style:

```php
<?php
// Connect to our social platform database  
// PDO is PHP's modern way to work with databases
$pdo = new PDO($dsn, $username, $password);

// Get all posts ordered by newest first
// This SQL query gets posts with user information
$sql = "SELECT p.*, u.username FROM posts p JOIN users u ON p.user_id = u.id ORDER BY p.created_at DESC";
$stmt = $pdo->prepare($sql);
$stmt->execute();
$posts = $stmt->fetchAll();

// Display each post
foreach ($posts as $post) {
    // Always escape user data to prevent XSS attacks
    echo "<h3>" . htmlspecialchars($post['title']) . "</h3>";
}
?>
```

#### Learning Aids:

- **💡 PHP Tip:** [Specific PHP knowledge]
- **⚠️ Security Note:** [Important security consideration]
- **🔗 Connection:** [How this relates to previous lessons]

### Section 2: Professional Focus

#### Comment Style:

```php
<?php
/**
 * PostController handles all post-related operations
 * 
 * @package SocialPlatform\Controllers
 */
class PostController
{
    private PostRepository $postRepo;

    public function __construct(PostRepository $postRepo)
    {
        $this->postRepo = $postRepo;
    }

    /**
     * Display paginated posts for the main feed
     */
    public function index(Request $request): Response
    {
        $posts = $this->postRepo->getPaginatedPosts(
            $request->get('page', 1)
        );

        return $this->render('posts/index', compact('posts'));
    }
}
?>
```

---

## Quality Checklist

### Before Publishing Any Lesson:

**Code Quality:**

- [ ] All code tested and working
- [ ] Under 100 lines of new code
- [ ] Clear, educational comments
- [ ] Security basics included
- [ ] Error handling present

**Educational Value:**

- [ ] Single clear learning objective
- [ ] PHP concepts explained clearly
- [ ] Practical application obvious
- [ ] Builds on previous lessons logically

**Consistency:**

- [ ] Uses established CSS classes
- [ ] Follows naming conventions
- [ ] Matches overall platform style
- [ ] References previous work accurately

### Testing Requirements:

- [ ] Code works on fresh LAMP setup
- [ ] All file permissions correct
- [ ] Database operations function properly
- [ ] Forms submit and validate correctly
- [ ] CSS classes render properly

---

## Time Management

### Typical Lesson Breakdown:

- **Understanding concepts:** 15-20 minutes
- **Hands-on coding:** 60-80 minutes
- **Testing and troubleshooting:** 15-20 minutes
- **Total:** 90-120 minutes

### Content Distribution:

- **Concept explanation:** 20%
- **Step-by-step coding:** 70%
- **Testing and review:** 10%

---

## File Organization Per Lesson

```
chapter-X/
├── styles.css (shared across chapter)
├── lesson-X.1/
│   ├── filename.php (main lesson file)
│   ├── additional-file.php (if needed)
│   └── README.md (lesson content)
└── lesson-X.2/
    └── [same structure]
```

This template ensures every lesson delivers working functionality while teaching PHP concepts efficiently within the 100-line constraint.
