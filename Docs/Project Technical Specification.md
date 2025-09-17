# Social Platform Project: Technical Specification

## Project Overview

**Project Name:** SocialHub (Generic social platform for learning PHP)  
**Purpose:** Educational project demonstrating modern PHP development  
**Design Philosophy:** Minimal UI, maximum functionality, dark theme  
**Target:** Deployable platform ready for student customization

---

## Core Features

### User System

- **Registration/Login:** Email-based with secure password handling
- **Profiles:** Basic info, bio, profile picture
- **Authentication:** Sessions, password reset, account management

### Content System

- **Posts:** Text content with optional images
- **Comments:** Threaded discussion on posts
- **Media:** Profile pictures and post images with upload handling

### Social Features

- **Following:** Users can follow/unfollow others
- **Likes:** Like posts and comments
- **Feed:** Timeline showing followed users' posts
- **Notifications:** Activity alerts for interactions

### Discovery & Management

- **Search:** Find users and content
- **Admin Panel:** Basic content and user management
- **API:** RESTful endpoints for all core functionality

---

## Technical Architecture

### Section 1: Simple Structure

```
/social-platform/
├── index.php (main feed)
├── login.php, register.php, profile.php
├── post.php, search.php, admin.php
├── api/ (JSON endpoints)
├── uploads/ (user media)
├── includes/ (shared components)
└── styles.css (single stylesheet)
```

### Section 2: Professional Structure

```
/social-platform/
├── public/ (web-accessible files)
├── src/ (application code)
│   ├── Controllers/
│   ├── Models/  
│   ├── Views/
│   └── Services/
├── config/ (environment settings)
├── database/ (migrations, seeds)
└── tests/ (automated testing)
```

---

## Database Schema

### Core Tables

```sql
users (
    id, username, email, password_hash,
    first_name, last_name, bio, avatar_url,
    created_at, updated_at
)

posts (
    id, user_id, content, image_url,
    created_at, updated_at  
)

comments (
    id, post_id, user_id, parent_id,
    content, created_at
)

likes (
    id, user_id, post_id, created_at
)

follows (  
    id, follower_id, following_id, created_at
)

notifications (
    id, user_id, type, data, is_read, created_at
)
```

### Design Principles

- **Simple relationships:** Minimal foreign keys
- **Standard naming:** snake_case, descriptive columns
- **Performance ready:** Basic indexes on common queries
- **Extensible:** Easy to add new features

---

## UI/UX Specification

### Design Philosophy

- **Dark theme throughout**
- **Minimal, functional design**
- **Mobile-responsive but desktop-first**
- **Reusable CSS classes**
- **No animations or complex styling**

### Core Components

```css
/* Base layout */
.container { max-width: 800px; margin: 0 auto; }
.card { background: #2a2a2a; padding: 20px; margin: 10px 0; }

/* Typography */  
.title { font-size: 1.5rem; color: #fff; }
.text { color: #ccc; line-height: 1.5; }
.muted { color: #888; font-size: 0.9rem; }

/* Interactive elements */
.btn { padding: 8px 16px; background: #444; color: #fff; }
.btn-primary { background: #007acc; }
.input { background: #333; color: #fff; padding: 8px; }
```

### Page Layout Standard

```html
<header class="site-header">
    <nav><!-- Navigation --></nav>
</header>
<main class="container">
    <div class="content"><!-- Page content --></div>  
</main>
<footer class="site-footer">
    <!-- Minimal footer -->
</footer>
```

---

## Feature Implementation Roadmap

### Section 1 Progression (8 Chapters)

**Chapter 1:** PHP basics + static content display  
**Chapter 2:** Database connection + user registration  
**Chapter 3:** Authentication + user sessions  
**Chapter 4:** Posts creation + social interactions  
**Chapter 5:** File uploads + media handling  
**Chapter 6:** Search + content discovery  
**Chapter 7:** API development + JSON endpoints  
**Chapter 8:** Security + production deployment

### Section 2 Professional Features

**Advanced Architecture:** MVC patterns, dependency injection  
**Professional Tools:** Composer, automated testing, Git workflow  
**Production Features:** Caching, monitoring, scalable deployment  
**Enterprise Security:** Advanced authentication, audit logging

---

## Code Complexity Targets

### Section 1 Guidelines

- **100 lines per lesson maximum** (excluding CSS file)
- **One CSS file per chapter** (shared across lessons)
- **Functional over elegant** - code that works first
- **Minimal dependencies** - mostly vanilla PHP

### Section 2 Guidelines

- **Professional patterns** - proper architecture
- **Modern PHP features** - type hints, namespaces, etc.
- **Industry standards** - PSR compliance, best practices
- **Production ready** - error handling, logging, monitoring

---

## Security Requirements

### Basic Security (Section 1)

- Password hashing with PHP's password_hash()
- SQL injection prevention with prepared statements
- XSS protection with htmlspecialchars()
- CSRF protection for forms
- File upload validation and security

### Advanced Security (Section 2)

- JWT token authentication
- Rate limiting and abuse prevention
- Security headers and CSP
- Input validation and sanitization libraries
- Security audit logging and monitoring

---

## Performance Considerations

### Section 1 Optimization

- **Basic caching:** Session-based page caching where appropriate
- **Image optimization:** Basic resizing and format validation
- **Query efficiency:** Simple joins, avoid N+1 problems
- **Minimal assets:** Single CSS file, minimal JavaScript

### Section 2 Optimization

- **Advanced caching:** Redis/Memcached integration
- **Database optimization:** Proper indexing, query optimization
- **Asset management:** Compression, CDN integration
- **Performance monitoring:** APM integration, metrics collection

---

## API Specification

### RESTful Endpoints (Section 1)

```
GET  /api/posts         - List posts
POST /api/posts         - Create post  
GET  /api/posts/{id}    - Get specific post
PUT  /api/posts/{id}    - Update post
DELETE /api/posts/{id}  - Delete post

GET  /api/users/{id}    - Get user profile
POST /api/auth/login    - User authentication
POST /api/auth/logout   - User logout

POST /api/posts/{id}/like    - Like a post
POST /api/users/{id}/follow  - Follow a user
```

### Response Format

```json
{
    "success": true,
    "data": { /* response data */ },
    "message": "Optional message",
    "meta": { 
        "pagination": {},
        "timestamp": "2024-01-15T10:30:00Z"
    }
}
```

---

## Success Criteria

### Section 1 Complete

- [ ] Full user registration and authentication
- [ ] Post creation with image uploads
- [ ] Social features (likes, comments, follows)
- [ ] Working search and discovery
- [ ] Complete API with documentation
- [ ] Basic admin panel
- [ ] Deployable to shared hosting
- [ ] Mobile responsive design

### Section 2 Complete

- [ ] Professional MVC architecture
- [ ] Comprehensive test coverage
- [ ] Production deployment pipeline
- [ ] Performance optimization implemented
- [ ] Security audit passed
- [ ] Monitoring and logging active
- [ ] Scalable for real-world usage

### Student Success Indicators

- Platform works immediately after following instructions
- Students can customize and extend features easily
- Code is readable and well-documented
- Deployment process is straightforward
- Students feel confident building similar projects

---

## Deployment Targets

### Section 1 Deployment

- **Shared hosting** (cPanel, standard LAMP)
- **Basic VPS** (DigitalOcean, Linode)
- **Local development** (XAMPP, MAMP)

### Section 2 Deployment

- **Cloud platforms** (AWS, Google Cloud, Azure)
- **Container deployment** (Docker, Kubernetes)
- **CI/CD pipelines** (GitHub Actions, GitLab CI)
- **Production monitoring** (logging, metrics, alerts)

This specification provides a clear technical roadmap while maintaining focus on practical PHP learning through building a real, working social platform.
