# Course Development Workflow & Consistency Guidelines

## Development Process

### Phase 1: Foundation ✅

- [x] Compact Table of Contents (8 chapters, Section 1)
- [x] Streamlined Project Specification
- [x] Lesson Template (100-line limit)
- [x] Code Style Guidelines (dark theme, reusable CSS)

### Phase 2: Content Development (Current)

- [ ] **Section 1:** Chapters 1-8 (40 lessons total)
- [ ] **Section 2:** Professional rebuild (variable length)
- [ ] **Appendices:** Quick references and troubleshooting

### Phase 3: Polish & Deploy

- [ ] Technical review and testing
- [ ] Consistency verification
- [ ] Student experience validation

---

## Core Consistency Rules

### Every Lesson Must Have:

```markdown
**Header:** Goal, time, prerequisites clearly stated
**100 lines max:** New PHP/HTML code (excluding shared CSS)
**One concept:** Single learning objective per lesson
**Working code:** Complete, tested, functional examples
**Dark theme:** Using established CSS classes only
```

### Every Chapter Must Have:

```css
/* styles.css - Shared across all 5 lessons in chapter */
/* Dark theme base with reusable classes */
/* Max 50-80 CSS rules total */
/* Build on previous chapters' styles */
```

### Code Quality Gates:

- [ ] **Functionality:** Code works on fresh LAMP stack
- [ ] **Security:** Basic protections (prepared statements, escaping, validation)
- [ ] **Readability:** Clear variable names, meaningful comments
- [ ] **Consistency:** Follows established naming and structure patterns

---

## Section-Specific Standards

### Section 1: Learning-Focused

**Comment Style:**

```php
// Connect to social platform database
// PDO is the modern, secure way to use databases in PHP
$pdo = new PDO($dsn, $username, $password);

// Get user posts with JOIN to combine tables
// This gets posts AND usernames in one efficient query
$sql = "SELECT p.*, u.username FROM posts p JOIN users u ON p.user_id = u.id";
```

**File Structure:**

```
chapter-X/
├── styles.css (shared)
├── config.php (database)  
├── functions.php (utilities)
└── lesson-files/
```

**Teaching Approach:**

- **Explain PHP concepts** with social platform context
- **Show before tell** - working code first, then explain why
- **Connect to previous work** - build on established foundation
- **Security from day 1** - never show insecure code, even temporarily

### Section 2: Professional-Focused

**Comment Style:**

```php
/**
 * PostController handles all post-related HTTP requests
 * 
 * @package SocialPlatform\Controllers
 */
class PostController extends BaseController
{
    /**
     * Display paginated posts for authenticated users
     */
    public function index(Request $request): Response
```

**File Structure:**

```
social-platform/
├── public/ (web accessible)
├── src/ (application code)
│   ├── Controllers/
│   ├── Models/
│   └── Services/
├── config/ (environment)
└── tests/ (automated testing)
```

**Professional Approach:**

- **Industry patterns** - MVC, dependency injection, proper architecture
- **Modern PHP** - type hints, namespaces, composer, testing
- **Production ready** - logging, monitoring, deployment pipelines
- **Real workflow** - Git, testing, code review, deployment

---

## CSS Consistency Framework

### Base Classes (Established in Chapter 1):

```css
/* Layout */
.container, .card, .flex

/* Typography */ 
.title, .text, .muted

/* Interactive */
.btn, .btn-primary, .input

/* Platform Components */
.post-card, .user-avatar, .nav-link
```

### Extension Pattern:

```css
/* Chapter 2: Add user-specific classes */
.user-profile, .profile-header

/* Chapter 3: Add form-specific classes */ 
.form-card, .error-message

/* Chapter 4: Add social interaction classes */
.like-button, .comment-form
```

### Rules:

- **Reuse existing classes** whenever possible
- **Extend, don't replace** - build on previous chapters
- **Keep dark theme consistent** - #1a1a1a background, #ccc text
- **No complex styling** - simple, functional design only

---

## Quality Checkpoints

### Per Lesson (Before Moving Forward):

- [ ] Code runs without errors on clean environment
- [ ] Under 100 lines of new code
- [ ] Uses existing CSS classes appropriately
- [ ] Security practices demonstrated correctly
- [ ] Learning objective clearly achieved
- [ ] Connects logically to previous and next lessons

### Per Chapter (Every 5 Lessons):

- [ ] Complete feature works end-to-end
- [ ] All previous functionality still works
- [ ] CSS file serves all lessons efficiently
- [ ] Chapter builds toward stated deliverable
- [ ] Time estimates are realistic and tested

### Section Complete:

- [ ] **Functional platform** - all core social features working
- [ ] **Security review** - protected against common vulnerabilities
- [ ] **Performance check** - loads quickly, handles multiple users
- [ ] **Deployment test** - works on shared hosting/basic VPS
- [ ] **Student success** - clear progression, achievable goals

---

## Development Workflow

### Starting a New Chapter:

1. **Review previous chapter** - ensure continuity
2. **Define chapter goal** - specific deliverable
3. **Plan CSS additions** - what new classes needed?
4. **Outline 5 lessons** - logical progression to goal
5. **Create styles.css** - based on previous chapter + new needs

### Creating Each Lesson:

1. **Define single learning objective**
2. **Write working code first** (test thoroughly)
3. **Add educational comments**
4. **Create step-by-step instructions**
5. **Test on fresh environment**
6. **Verify 100-line limit**

### Before Publishing:

1. **Functionality test** - works as intended
2. **Security review** - no vulnerabilities introduced
3. **Consistency check** - matches established patterns
4. **Time validation** - realistic completion time
5. **Next lesson setup** - clear connection established

---

## Student Experience Guidelines

### Success Indicators:

- **Code works immediately** when following instructions
- **Students see results quickly** - functional features each lesson
- **Questions focus on extension** rather than "why doesn't this work"
- **High completion rates** through difficult concepts
- **Students customize their platforms** - evidence they understand

### Red Flags to Avoid:

- **Time overruns** - lessons taking much longer than estimated
- **Repeated debugging** - same students stuck on same issues
- **Design complexity** - students lost in CSS instead of learning PHP
- **Feature creep** - lessons trying to do too much at once
- **Security gaps** - vulnerable code patterns, even temporarily

---

## Communication Patterns

### Connecting Lessons:

- **"Building on Chapter X..."**
- **"Remember when we created X in Lesson Y..."**
- **"This follows the same pattern as..."**
- **"You'll find this in your existing filename.php..."**

### Teaching New Concepts:

- **"Here's what we're building and why..."**
- **"The PHP concept we need is..."**
- **"In our social platform, this means..."**
- **"Let's see this working first, then understand how..."**

### Handling Complexity:

- **"We'll keep this simple for now..."**
- **"In Section 2, we'll build this professionally..."**
- **"The important thing to understand is..."**
- **"Don't worry about X yet, focus on Y..."**

---

## Technical Standards

### Database Consistency:

```sql
-- Always: plural table names, snake_case columns
users, posts, comments, likes, follows

-- Always: standard field patterns
id (AUTO_INCREMENT PRIMARY KEY)
user_id (foreign key reference)  
created_at (TIMESTAMP DEFAULT CURRENT_TIMESTAMP)
```

### PHP Consistency:

```php
// Always: snake_case variables matching database
$user_name, $post_content, $created_at

// Always: prepared statements
$stmt = $pdo->prepare("SELECT * FROM users WHERE id = ?");
$stmt->execute([$user_id]);

// Always: escape output  
echo htmlspecialchars($user_input, ENT_QUOTES, 'UTF-8');
```

### File Naming:

```
// Section 1: descriptive, simple
login.php, register.php, user-profile.php, post-feed.php

// Section 2: professional structure  
UserController.php, PostRepository.php, AuthService.php
```

---

## Version Control Strategy

### Branch Structure:

- **main:** Completed, tested lessons ready for students
- **chapter-X:** Development of specific chapters
- **review:** Content under technical review

### Commit Messages:

```
Chapter 1.1: PHP basics and first dynamic page - Initial draft
Chapter 1: Complete and tested - All 5 lessons working
Section 1: Complete foundation - Ready for student testing
```

---

## Success Metrics

### Course Quality:

- **Consistent completion times** (±30 minutes from estimates)
- **High functionality success rate** (code works for 90%+ of students)
- **Low correction/revision rate** (lessons work correctly first time)
- **Progressive difficulty curve** (each lesson slightly more challenging)

### Student Outcomes:

- **Platform customization** (students modify/extend their version)
- **Concept application** (students use learned concepts in new ways)
- **Confidence building** (students feel ready to tackle new PHP projects)
- **Real deployment** (students actually put their platform online)

### Technical Excellence:

- **Security standards maintained** throughout all lessons
- **Performance remains good** as platform grows in complexity
- **Code quality consistent** across all chapters and sections
- **Modern PHP practices** demonstrated from beginning to end

---

## Final Consistency Check

Before course launch, verify:

- [ ] **All 40 lessons** follow template exactly
- [ ] **Dark theme maintained** across all chapters
- [ ] **100-line limits respected** in every lesson
- [ ] **CSS classes reused** appropriately throughout
- [ ] **Security practices** never compromised for simplicity
- [ ] **Learning objectives** clearly met in each lesson
- [ ] **Platform functionality** works completely end-to-end
- [ ] **Student experience** tested with real users

This workflow ensures a consistently excellent course that teaches modern PHP through building something genuinely useful.
