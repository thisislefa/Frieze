# Frieze - Modern Blog Grid Component

A responsive, animated blog post grid component featuring a clean design with interactive elements and view counter animations. This component showcases blog posts with visual badges, author information, and animated view statistics.

## Live Preview

[View Live Demo](https://thisislefa.github.io/Frieze/) | [GitHub Repository](https://github.com/thisislefa/Frieze)

## Overview

Frieze is a modern blog post grid component designed for content-heavy websites. It features a responsive 3-column layout that adapts to different screen sizes, animated view counters, and hover effects for enhanced user engagement. The component emphasizes clean typography and visual hierarchy while maintaining optimal performance.

## Features

- **Responsive 3-Column Grid**: Adapts to 2 columns on tablets and 1 column on mobile
- **Animated View Counters**: Smooth number counting animation triggered on scroll
- **Glassmorphism Badges**: Semi-transparent category labels with backdrop blur
- **Hover Effects**: Image scaling and title color transitions
- **Performance Optimized**: Intersection Observer for scroll-based animations
- **Accessibility Ready**: Semantic HTML, proper alt text, and keyboard navigation
- **Typography Hierarchy**: Carefully sized text with optimal line heights
- **Image Aspect Ratio**: Consistent 16:10 image containers with object-fit

## Project Structure

```
Frieze/
├── index.html          # Complete HTML structure with inline JavaScript
├── style.css          # All styling with CSS variables and animations
└── READme.md          # This documentation
```

## Installation & Usage

### Quick Integration

```html
<!-- Include in your project -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<link rel="stylesheet" href="path/to/frieze.css">

<section class="blog-section">
  <!-- Copy grid structure from index.html -->
</section>

<script src="path/to/frieze.js"></script>
```

### Customization Options

#### CSS Variables
Modify the design system by updating these variables:

```css
:root {
  --color-text-primary: #111827;    /* Primary text color */
  --color-text-secondary: #4B5563;  /* Secondary text color */
  --color-text-light: #9CA3AF;      /* Light text/statistics */
  --color-bg-badge: rgba(255, 255, 255, 0.25); /* Glass badge background */
  --color-badge-border: rgba(255, 255, 255, 0.3); /* Badge border */
  --font-family: 'Inter', sans-serif; /* Primary font */
  --spacing-container: 120px;        /* Section padding */
  --spacing-card-gap: 32px;          /* Grid gap between cards */
}
```

#### Adding More Blog Posts
Extend the grid by adding more article elements:

```html
<article class="blog-card">
  <div class="card-media-wrapper">
    <span class="card-badge">Category</span>
    <img src="image-url.jpg" alt="Description" class="card-image">
  </div>
  <div class="card-content">
    <h3 class="card-title">Blog Post Title</h3>
    <footer class="card-footer">
      <div class="author-info">
        <img src="author-avatar.jpg" alt="Author Name" class="author-avatar">
        <span class="author-name">Author Name</span>
      </div>
      <div class="post-meta">
        <time class="post-date">DD.MM.YYYY</time>
        <div class="post-stats">
          <span class="stat-icon">
            <!-- Eye icon SVG -->
          </span>
          <span class="stat-number" data-target="1000">0</span>
        </div>
      </div>
    </footer>
  </div>
</article>
```

## Technical Implementation

### Responsive Grid System

The component uses CSS Grid with media queries for responsive behavior:

```css
.blog-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr); /* Desktop: 3 columns */
  gap: var(--spacing-card-gap);
}

@media (max-width: 1024px) {
  .blog-grid {
    grid-template-columns: repeat(2, 1fr); /* Tablet: 2 columns */
  }
}

@media (max-width: 768px) {
  .blog-grid {
    grid-template-columns: 1fr; /* Mobile: 1 column */
  }
}
```

### Animated View Counters

The view counters use JavaScript to animate from 0 to their target value:

```javascript
// Configuration
const speed = 90; // Animation speed (lower = slower)
const counters = document.querySelectorAll('.stat-number');

// Intersection Observer triggers animation
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      animateCounters();
      observer.disconnect();
    }
  });
}, { threshold: 0.5 });
```

### Glassmorphism Effect

The category badges use modern CSS properties for a glass-like appearance:

```css
.card-badge {
  background: var(--color-bg-badge);
  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
  border: 1px solid var(--color-badge-border);
}
```

## JavaScript API

### Available Configuration

The animation script can be customized with these parameters:

```javascript
// In the script section of index.html
const speed = 90; // Adjust animation speed
const threshold = 0.5; // Intersection Observer threshold (0-1)
const delay = 20; // Update interval in milliseconds
```

### Manual Animation Trigger

To manually trigger animations without scrolling:

```javascript
// Call this function anywhere in your code
function triggerCounterAnimation() {
  const counters = document.querySelectorAll('.stat-number');
  // ... animation logic from index.html
}
```

## Performance Optimization

1. **Image Optimization**: Uses Unsplash CDN with auto-format and crop parameters
2. **Lazy Loading**: Consider adding `loading="lazy"` to images
3. **CSS Containment**: Cards use `overflow: hidden` for better rendering
4. **Efficient Animations**: Uses `transform` and `opacity` for GPU acceleration
5. **Font Loading**: Preconnects to Google Fonts for faster loading

## Accessibility Features

- **Semantic HTML**: Uses `<article>`, `<time>`, and proper heading hierarchy
- **ARIA Labels**: Interactive elements have appropriate labels
- **Keyboard Navigation**: All interactive elements are focusable
- **Color Contrast**: Meets WCAG AA standards for text readability
- **Focus States**: Buttons and links have visible focus indicators
- **Alt Text**: All images have descriptive alt attributes

## Browser Support

- Chrome 60+
- Firefox 55+
- Safari 12+
- Edge 79+
- iOS Safari 12+
- Android Chrome 67+

**Note**: The glassmorphism effect (`backdrop-filter`) may not work in older browsers but gracefully degrades.

## Customization Examples

### Changing Color Scheme

```css
/* Dark theme variant */
.dark-theme .blog-section {
  background-color: #1a1a1a;
}

.dark-theme .card-title {
  color: #ffffff;
}

.dark-theme .author-name {
  color: #cccccc;
}
```

### Different Layout Variations

```css
/* 4-column layout for larger screens */
@media (min-width: 1400px) {
  .blog-grid {
    grid-template-columns: repeat(4, 1fr);
  }
}

/* Masonry layout alternative */
.masonry-grid {
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  grid-auto-rows: masonry;
}
```

### Adding Reading Time

```html
<div class="post-meta">
  <time class="post-date">08.08.2025</time>
  <span class="reading-time">5 min read</span>
  <div class="post-stats">
    <!-- Existing view counter -->
  </div>
</div>
```

## Troubleshooting

### Common Issues

1. **Counters not animating**: Ensure the Intersection Observer threshold is appropriate for your layout
2. **Images not loading**: Check image URLs and network connectivity
3. **Layout breaks on mobile**: Verify viewport meta tag is present
4. **Glass effect not working**: Browser may not support `backdrop-filter`

### Debug Mode

Add this to your browser console to debug the component:

```javascript
// Check if counters are properly initialized
console.log('Total counters:', document.querySelectorAll('.stat-number').length);

// Check Intersection Observer status
const section = document.querySelector('.blog-section');
const rect = section.getBoundingClientRect();
console.log('Section visibility:', {
  top: rect.top,
  bottom: rect.bottom,
  windowHeight: window.innerHeight
});
```

## Extending the Component

### API Integration

To dynamically load blog posts from an API:

```javascript
async function loadBlogPosts() {
  try {
    const response = await fetch('/api/blog-posts');
    const posts = await response.json();
    
    const grid = document.querySelector('.blog-grid');
    grid.innerHTML = posts.map(post => createPostHTML(post)).join('');
    
    // Re-initialize animations
    initializeCounters();
  } catch (error) {
    console.error('Failed to load blog posts:', error);
  }
}
```

### Adding Pagination

```html
<div class="pagination">
  <button class="pagination-btn prev">Previous</button>
  <span class="page-info">Page 1 of 3</span>
  <button class="pagination-btn next">Next</button>
</div>
```

## License

MIT License - Free for personal and commercial use with attribution.

## Author

**Lefa Mofokeng**  
GitHub: [@thisislefa](https://github.com/thisislefa)

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/enhancement`)
3. Commit changes (`git commit -m 'Add new feature'`)
4. Push to branch (`git push origin feature/enhancement`)
5. Open a Pull Request

---

Frieze provides a robust foundation for blog post displays with modern design patterns and interactive elements. The component is production-ready and easily customizable for various content strategies.
