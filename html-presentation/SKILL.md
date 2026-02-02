---
name: html-presentation
description: Create professional HTML-based presentations and slides. Use this skill when the user asks to build presentations, slides, slide decks, or educational content in web format (examples include technical tutorials, training materials, product demos, conference presentations, or documentation). Generates interactive, cross-platform HTML presentations with navigation and animations.
license: Complete terms in LICENSE.txt
---

This skill guides creation of professional HTML-based presentations that are cross-platform, interactive, and easily shareable.

The user provides presentation requirements: topic, content, structure, or a draft to convert into HTML presentation format.

## HTML Presentation Advantages

HTML Presentations offer significant advantages over traditional PowerPoint:
- **Cross-platform**: Opens in any browser on any device
- **Small file size**: Pure text files, typically KB vs MB
- **Easy sharing**: Share via web link or simple HTML file
- **Interactive**: JavaScript enables unlimited interactivity
- **Version control**: Track changes with Git
- **Cost-free**: No expensive software required

## Technical Architecture

### HTML Structure
```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Presentation Title</title>
    <style>
        /* CSS styles */
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>Title</h1>
            <div class="subtitle">Subtitle</div>
        </div>

        <div class="content">
            <!-- Slides go here -->
        </div>

        <div class="progress">
            Slide <span id="currentSlide">1</span> / <span id="totalSlides">10</span>
        </div>

        <div class="navigation">
            <button class="nav-btn" id="prevBtn">← Previous</button>
            <button class="nav-btn" id="nextBtn">Next →</button>
        </div>
    </div>

    <script>
        // Navigation logic
    </script>
</body>
</html>
```

### CSS Layout Best Practices

#### Container Setup
```css
body {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px;
}

.container {
    max-width: 1200px;
    width: 100%;
    background: white;
    border-radius: 20px;
    box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
    overflow: hidden;
}
```

#### Slide System
```css
.slide {
    display: none;
    animation: fadeIn 0.5s ease-in-out;
}

.slide.active {
    display: block;
}

@keyframes fadeIn {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
}
```

#### **CRITICAL: Flowchart/Diagram Layout**
All flowcharts and diagrams MUST use Flexbox, never `inline-block`:

```css
.diagram {
    background: #f8f9fa;
    padding: 30px;
    border-radius: 10px;
    margin: 20px 0;
    text-align: center;
    display: flex;           /* REQUIRED: Use flexbox */
    align-items: center;     /* REQUIRED: Center vertically */
    justify-content: center; /* REQUIRED: Center horizontally */
    flex-wrap: wrap;         /* OPTIONAL: Allow wrapping on small screens */
}

.diagram-box {
    background: white;
    border: 3px solid #667eea;
    padding: 15px;
    margin: 10px;
    border-radius: 8px;
    flex-shrink: 0;          /* REQUIRED: Prevent compression */
    min-width: 150px;
}

.arrow {
    font-size: 2em;
    color: #764ba2;
    flex-shrink: 0;          /* REQUIRED: Prevent compression */
}
```

**Why Flexbox?**
- `inline-block` is sensitive to whitespace and line breaks in HTML
- Unpredictable spacing across browsers
- Flexbox provides reliable, consistent alignment
- Better control over wrapping behavior

#### Common UI Components

**Highlight Box:**
```css
.highlight-box {
    background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
    border-left: 5px solid #667eea;
    padding: 20px;
    margin: 20px 0;
    border-radius: 5px;
}
```

**Key Point Box:**
```css
.key-point {
    background: linear-gradient(135deg, #ffeaa7 0%, #fdcb6e 100%);
    color: #2d3436;
    padding: 15px;
    border-radius: 8px;
    margin: 15px 0;
    font-weight: bold;
}
```

**Feature Box:**
```css
.feature-box {
    background: #f8f9fa;
    border: 2px solid #667eea;
    padding: 20px;
    margin: 15px 0;
    border-radius: 10px;
}
```

**Grid Layouts:**
```css
.stat-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
    margin: 30px 0;
}

.tech-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 20px;
    margin: 20px 0;
}
```

**Comparison Table:**
```css
.comparison-table {
    width: 100%;
    border-collapse: collapse;
    margin: 20px 0;
}

.comparison-table th,
.comparison-table td {
    padding: 12px;
    text-align: left;
    border-bottom: 1px solid #dee2e6;
}

.comparison-table th {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
}

.comparison-table tr:hover {
    background: #f3f4f6;
}
```

### JavaScript Navigation

```javascript
let currentSlide = 1;
const totalSlides = 10;

function changeSlide(direction) {
    const slides = document.querySelectorAll('.slide');
    slides[currentSlide - 1].classList.remove('active');

    currentSlide += direction;

    if (currentSlide < 1) currentSlide = 1;
    if (currentSlide > totalSlides) currentSlide = totalSlides;

    slides[currentSlide - 1].classList.add('active');

    document.getElementById('currentSlide').textContent = currentSlide;
    document.getElementById('prevBtn').disabled = currentSlide === 1;
    document.getElementById('nextBtn').disabled = currentSlide === totalSlides;
}

// Keyboard navigation
document.addEventListener('keydown', function(event) {
    if (event.key === 'ArrowRight' || event.key === ' ') {
        changeSlide(1);
    } else if (event.key === 'ArrowLeft') {
        changeSlide(-1);
    }
});

// Initialize button state
document.getElementById('prevBtn').disabled = true;
```

## Design Guidelines

### Typography
- **Headers**: 2-2.5em for h1, 1.5-2em for h2, 1.2-1.5em for h3
- **Body**: 1.05-1.1em for readability
- **Line height**: 1.8 for body text
- **System fonts**: Use `-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto` for native feel

### Color Themes
Choose cohesive color schemes using CSS variables:
- **Primary**: For headers, buttons, borders
- **Secondary**: For accents, highlights
- **Gradients**: Use subtle gradients for depth
- **Backgrounds**: White cards on gradient backgrounds work well

Avoid clichéd purple gradients (#667eea to #764ba2) - vary colors based on content and context.

### Animations
- **Fade-in**: Use for slide transitions
- **Hover effects**: Transform translateY with box-shadow
- **Stagger reveals**: Use animation-delay for list items
- Keep animations subtle (0.3-0.5s duration)

### Accessibility
- Ensure high contrast ratios
- Use semantic HTML (h1-h6, nav, section)
- Provide keyboard navigation
- Include aria-labels where needed
- Test with screen readers

## Content Structure

### Slide Organization
1. **Title slide**: Introduction with overview
2. **Agenda/Outline**: Table of contents
3. **Content slides**: 3-5 main sections, each with multiple slides
4. **Examples/Demos**: Code blocks, diagrams, interactive elements
5. **Summary**: Key takeaways
6. **Q&A / Next Steps**: Conclusion and resources

### Visual Hierarchy
- Use h2 for slide titles
- Use h3 for section headers within slides
- Use bullet points for lists
- Highlight key information with colored boxes
- Use diagrams for complex concepts

## Common Use Cases

### Technical Training
- Code examples with syntax highlighting
- Architecture diagrams
- Step-by-step tutorials
- Best practices checklists

### Product Demos
- Feature highlights
- Use case scenarios
- Comparison tables
- Screenshots/mockups

### Educational Content
- Concept explanations
- Historical timelines
- Process flows
- Case studies

## File Organization

For multi-chapter presentations:
- Separate HTML file per chapter
- Consistent navigation and styling
- Include a complete/merged version
- Use descriptive filenames (e.g., `01_Introduction.html`)

## Best Practices

1. **Keep slides focused**: One main idea per slide
2. **Use visuals**: Diagrams, icons, and color coding improve retention
3. **Maintain consistency**: Use the same styling throughout
4. **Test thoroughly**: Check on multiple browsers and screen sizes
5. **Provide context**: Include title, progress indicator, and navigation
6. **Optimize file size**: Minimize external dependencies
7. **Add interactivity**: Hover effects, animations, keyboard shortcuts
8. **Include metadata**: Title, description, language tags

## Export Options

- **HTML**: Single file, easiest to share
- **PDF**: Print from browser for offline distribution
- **PDF via wkhtmltopdf**: Command-line conversion
- **Hosting**: Deploy to GitHub Pages, Netlify, or any web server

Remember: HTML presentations are powerful because they combine the structure of slides with the flexibility of the web. Leverage this by creating interactive, engaging content that goes beyond static slides.
