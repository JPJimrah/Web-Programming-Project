# Technical Report

## 1. Visual Design Rationale

### 1.1 Design Philosophy

The portfolio adopts a Minimalist Modern visual language rather than a terminal-inspired dark-tech aesthetic. The selected approach is intentionally clean, academically professional, and technically credible for a future Computer Engineer from Ahmadu Bello University, Zaria. The interface uses generous white space, structured content blocks, and highly legible typography to present the student's identity as disciplined, dependable, and technically focused.

This choice fits the portfolio purpose well because a student engineering portfolio should communicate clarity, competence, and trust. The dominant green theme reflects growth, reliability, and technical confidence, while the white and neutral panels keep the interface fresh and readable. The result is a professional page structure that feels appropriate for an academic and engineering profile without becoming visually noisy or overly decorative.

### 1.2 Color and Typography

The actual CSS palette used across the site is specific and consistent:

- Main background: `#f4faf6`
- Primary text: `#222222`
- Header, navigation, and dark structural accents: `#0a4d2c`
- White content surfaces: `#ffffff`
- Alternate content backgrounds: `#e6f4ea`
- Headings and accent borders: `#0b6e3f`
- Button and primary action blue: `#075985`
- Button hover: `#0c4a6e`
- Border color for cards and forms: `#cbd5e1`
- Warning notice border accent: `#c9a227`
- Interest card backgrounds: `#0a4d2c`, `#7c5c32`, `#075985`, `#6b3f75`, and `#9a3412`

These choices support high readability and strong contrast. For example, the combination of `#222222` text on `#f4faf6` background provides a high-contrast reading surface suitable for normal body text, and the use of `#ffffff` text on `#0a4d2c` and `#075985` yields strong contrast for headers, navigation, and action controls. These values are compliant with WCAG AA expectations for standard text contrast, making the portfolio accessible in a way that aligns with web usability principles.

The typography system is intentionally simple and functional. The base body font is declared as: `font-family: Arial, Helvetica, sans-serif;` This is a sans-serif stack chosen for clarity, modernity, and legibility across browser environments. The hierarchy is built around a strong heading structure: the main header name uses a large, responsive scale via `clamp(2rem, 6vw, 3rem)`, while section headings are visually emphasized with a green underline. The page avoids decorative or overly stylized fonts to maintain professionalism and high readability. In other words, the type system favors function over ornament, which is appropriate for a technical portfolio and matches the engineering identity of the content.

### 1.3 CSS Layout System

The site uses a hybrid CSS layout strategy based on Flexbox and Grid, rather than external frameworks such as Bootstrap or Tailwind. This was a deliberate architectural decision to keep the project fully static, dependency-free, and aligned with the assignment constraints. The CSS is hand-crafted to provide structure without any JavaScript or framework overhead, which makes the site easy to maintain and simple to host on any static server.

Examples from the implemented stylesheet include:

- `body { display: flex; flex-direction: column; }` to stack header, nav, main, and footer in a consistent vertical flow.
- `nav ul { display: flex; flex-wrap: wrap; justify-content: center; }` to create a responsive navigation bar that can wrap naturally on smaller screens.
- `.project-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); }` to arrange project cards in flexible columns.
- `.skills-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); }` for technical skill grouping.
- `main dl { display: grid; grid-template-columns: minmax(120px, 0.4fr) minmax(0, 1fr); }` for a structured key-value layout.

The responsive breakpoints in the stylesheet are narrow, simple, and practical. The key media query is:

- `@media (max-width: 700px) { ... }`

Within this breakpoint, the stylesheet reduces grid complexity, makes definitions stack more cleanly, and optimizes navigation and content blocks for narrow mobile viewports. This is a classic mobile-first adaptation strategy in a static CSS environment: the base layout is designed for larger screens and then simplified for smaller screens at the 700px threshold.

### 1.4 Pure CSS Interactivity

The site implements interactivity without JavaScript by using CSS pseudo-classes and anchor-based state changes. The most important example is the project detail modal. Each project card contains a link such as `href="#project-1"`, and each modal section is given an ID such as `#project-1`.

The relevant logic is:

- `.project-modal { visibility: hidden; opacity: 0; pointer-events: none; }`
- `.project-modal:target { visibility: visible; opacity: 1; pointer-events: auto; }`
- `.project-modal:target .modal-panel { transform: translateY(0); }`

This means that when the URL hash matches the modal ID, the corresponding modal becomes visible. The close button links back to `projects.html`, which removes the hash target and hides the overlay again. This is a clean CSS-only state-management pattern that adheres strictly to the no-JavaScript requirement.

The same philosophy could be used for accordions with the `:checked` pseudo-class on hidden inputs, but the actual project does not require this pattern because the site relies on anchor-target modal overlays. In both cases, the objective is same: manage UI state through CSS selectors rather than client-side script, preserving simplicity, speed, and compliance with the project constraints.

---

## 2. System Architecture and Design

The website follows a simple static architecture. Each page is a standalone HTML document that includes the same page skeleton: a header, navigation, main content area, and footer. The styling is shared globally through a single stylesheet, which ensures consistent visual identity across the entire project.

### 2.1 Page Structure

The architecture demonstrates a modular design approach, even though it is static. Common elements are repeated across pages without requiring server-side templating. The overall structure of each document includes:

- `head` section with metadata and page title
- `header` containing the profile image, name, and short professional line
- `nav` with links to all main portfolio sections
- `main` content area containing the page-specific material
- `footer` with copyright and contact details

This pattern allows for effective consistency and easier maintenance. It also makes the site straightforward to host on static web hosting, GitHub Pages, or any simple file server.

### 2.2 Styling and Visual Design

The CSS file defines a restrained visual language built around a green, white, and neutral palette. The primary color scheme uses dark green for header and navigation styling, white content panels, and subtle green backgrounds for alternating sections. A default sans-serif type family is used, and responsive layout mechanisms are implemented with CSS grid, flexbox, and media queries.

Key CSS features include:

- `display: flex` and `display: grid` for layout structure;
- `clamp()` sizing for scalable responsive headings;
- `object-fit: cover` for profile and project images;
- sticky visual hierarchy for headings and section blocks;
- `@media (max-width: 700px)` responsive rules for narrow screens;
- modal styles for project detail popups using CSS `:target` behavior.

The design strongly reflects a portfolio rather than a commercial app, with emphasis on readability, academic professionalism, and a clean engineering aesthetic.

### 2.3 Navigation and Accessibility

The navigation is implemented using a standard HTML list within a `<nav>` element and includes links to all pages. This creates a clear site map and consistent user movement across the portfolio. Each page includes semantic headings (`h1`, `h2`, `h3`), descriptive alt text for images, and labels for form controls.

The contact page includes a standard HTML form with `method="post"`, input validation attributes, and accessible label associations. The project pages use modal sections triggered by anchor links, offering a lightweight way to display additional content without JavaScript.

---

## 3. Implementation Details and Data Model

### 3.1 HTML Implementation

The page content reflects the actual portfolio content of the student. The home page introduces the student as a final-year Computer Engineering student focused on robotics, embedded systems, software development, and Linux. It also identifies the current final-year project: an autonomous delivery robot with obstacle avoidance, sensors, motors, and Bluetooth control.

The about page provides a more in-depth personal profile, emphasizing web programming, hardware-software integration, embedded systems, and future engineering goals. The education page records academic history from primary school through final-year engineering study and identifies relevant coursework such as Web Programming, Software Engineering, and Microprocessor Systems.

The skills page lists technical competencies grouped into categories:

- Programming Languages: HTML5, CSS3, JSON, Python, C++, Assembly
- Web Technologies: semantic HTML, responsive CSS, Flexbox, Grid, accessible forms
- Software Tools: Linux, MATLAB, Simulink, Stateflow, Git, technical documentation
- Hardware and Embedded Systems: Arduino programming, sensor integration, Bluetooth communication, motor control

The projects page contains five projects: Autonomous Delivery Robot, Growth Mentorship Programme, IoT-Based Smart Tomato Irrigation System, Guidance and Counseling App, and Personal Portfolio Website. Each card includes category, project date, description, and a detail view link. The hobbies page covers IoT experimentation, learning, reading, robotics, and teaching. The CV page summarizes the professional profile, education, experience, skills, and community development focus.

### 3.2 CSS Implementation

The CSS file is not a framework build; it is a handcrafted stylesheet that controls the full appearance of the portfolio. It defines:

- global resets and sizing rules;
- the color palette and text styling;
- header and footer structure;
- content card and section styling;
- responsive navigation layout;
- project-grid and skills-grid presentation;
- table formatting for education details;
- modal and form design;
- media-query adjustments for smaller screens.

This reveals a pragmatic, front-end engineering approach where style rules are intentionally defined for a specific portfolio rather than generated by a template system.

### 3.3 JSON Data Structure

The project data is stored in `data/data.json` and includes two main arrays:

- `projects`
- `education`

The `projects` array contains five entries, each with:

- `id`
- `title`
- `date`
- `category`
- `description`
- `image_url`

The `education` array includes three academic records with:

- `id`
- `institution`
- `start_date`
- `end_date`
- `qualification`
- `description`

This JSON file is a clear demonstration of structured content storage, showing how data can remain separate from presentation logic. Although this project does not currently render JSON into the page dynamically, the data model is consistently organized and suitable for future expansion or programmatic rendering.

---

## 4. Evaluation, Testing, and Limitations

### 4.1 Technical Evaluation

The implementation satisfies the core requirements of a static, lightweight portfolio site. It is easy to navigate, visually coherent, and technically appropriate for a course-level web project. The absence of JavaScript means the site is highly portable and fast to load; the absence of external frameworks keeps the architecture simple and transparent.

The project demonstrates acceptable HTML5 semantics, CSS layout design, and content structuring. The use of `aria-label`, `alt` text, labels, and accessible form controls shows consideration for usability and accessibility. The use of one stylesheet for all pages also reduces duplication and improves maintainability.

### 4.2 Testing and Validation Considerations

The site was inspected against the actual implemented code and content. The following technical facts were confirmed:

- The project is a static multi-page website.
- The design uses CSS-only layout styling and no JavaScript-driven interaction logic.
- Project and education content is represented in `data/data.json` and aligned with page descriptions.
- There are eight main portfolio pages and a shared stylesheet.
- The contact form is configured as an HTML form using standard `POST` submission behavior.
- Project modal views are implemented with CSS `:target` selectors, not JavaScript.

These checks confirm that the report reflects the actual codebase rather than an assumed or aspirational architecture.

### 4.3 Limitations and Future Improvements

Although the portfolio is complete and functional as a static website, it has several opportunities for enhancement:

- JSON could be consumed dynamically to reduce repeated project content in HTML.
- Additional interactivity could be introduced with JavaScript if allowed in future versions.
- More advanced responsive behavior could be added for mobile-first polish.
- The site could be expanded to include downloadable CVs, certifications, or a project gallery with real images and descriptions.

Despite these future improvements, the current implementation is a strong example of a structured static web solution in a Computer Engineering academic context.

## 2. Data Structure Definitions & Semantic Metadata

### 2.1 JSON Content Schema

The site stores structured content in `/data/data.json`, which acts as a machine-readable content model for the portfolio. This file is intentionally simple and explicit, separating content definitions from the presentation layer so that the HTML pages remain readable and maintainable.

The JSON structure contains two top-level arrays:

- `projects`
- `education`

#### Projects schema

Each project entry is represented as an object with the following properties:

- `id`: numeric identifier for the project entry
- `title`: the name of the project
- `date`: the year or status label (for example, `Current`, `2026`, `2025`)
- `category`: a classification such as `Robotics`, `Mentorship`, `Internet of Things`, `Mobile App`, or `Web Development`
- `description`: a short summary of the project outcome or purpose
- `image_url`: a relative path to the associated image asset

This definition is reflected in the actual JSON file, which contains five entries:

- Autonomous Delivery Robot
- Growth Mentorship Programme
- IoT-Based Smart Tomato Irrigation System
- Guidance and Counseling App
- Personal Portfolio Website

Each object is designed to be directly readable by both humans and future scripts. The schema is lightweight but sufficiently structured to support content rendering in other contexts, such as a CMS, a template engine, or future automated portfolio generation.

#### Education schema

The `education` array stores academic history as structured records with the following properties:

- `id`: unique numeric identifier
- `institution`: school or university name
- `start_date`: start of academic period
- `end_date`: end or expected completion period
- `qualification`: programme or level attained
- `description`: short textual description of the educational record

The actual file contains three records covering:

- Peace Nursery/Primary School, Maryam, Tafawa Balewa
- COCIN Metropolitan Unity Secondary School, Tafawa Balewa LGA
- Ahmadu Bello University, Zaria

This schema is useful because it separates factual academic data from visual presentation. In a larger system, the same data could be consumed by a templated HTML page, a mobile app, or a JSON-driven dashboard without redefining the content source.

### 2.2 Semantic Linked Data (JSON-LD)

The homepage includes a `script` tag in the `<head>` section of `index.html` with type `application/ld+json`. This is a standard method for embedding Schema.org metadata directly into HTML so that search engines and indexing systems can understand the page’s structured data without the need for JavaScript.

The embedded object is a `Person` record from Schema.org:

- `@context`: `https://schema.org`
- `@type`: `Person`
- `name`: `Jimrah Peter Jimrah`
- `jobTitle`: `Computer Engineering Student`
- `description`: final-year Computer Engineering student at Ahmadu Bello University, Zaria
- `fieldOfStudy`: `Computer Engineering`
- `affiliation`: university object with `@type` set to `CollegeOrUniversity`
- `sameAs`: LinkedIn profile URL

The reason this is important is that search engine crawlers can parse JSON-LD directly from the raw HTML document when the page loads. They do not need client-side JavaScript execution to see the structured data. This improves discoverability, allows rich indexing, and gives the website a machine-readable profile of the owner.

In practical terms, the JSON-LD block tells the web crawler: “This page represents a person named Jimrah Peter Jimrah, who is a Computer Engineering student affiliated with Ahmadu Bello University, and whose public profile is on LinkedIn.” That structured representation is useful for knowledge graph indexing, search relevance, and semantic interpretation by crawlers such as Google and other search engines.

This design is highly appropriate for a static portfolio because it requires no framework or runtime logic; the data is placed directly in the markup and is immediately machine-readable to crawlers. It also fits the project constraints of a pure HTML/CSS/JSON architecture without adding JavaScript dependency or backend processing.

## 3. HTTP/HTTPS Protocols & MIME Types Overview

### 3.1 Asset Delivery via HTTP/HTTPS

The portfolio is a static website, so browser communication is based on standard HTTP or HTTPS request/response cycles. When a user opens a page such as `index.html` or navigates to `projects.html`, the browser sends a request to the web server for the relevant resource. The server then replies with an HTTP response that includes a status code, headers, and the resource body.

For this project, the sequence is straightforward:

1. The browser resolves the requested URL and opens a TCP connection to the web server.
2. It sends an HTTP `GET` request for a specific resource, such as `/index.html`, `/assets/css/style.css`, `/data/data.json`, or an image file like `/assets/images/jp.jpg`.
3. The server locates the file on disk and prepares an HTTP response.
4. The response includes important headers, including the `Content-Type` header that tells the browser what kind of document it is receiving.
5. The browser reads the response and decides how to process the content:
   - HTML files are parsed as DOM documents.
   - CSS files are interpreted as stylesheet rules.
   - JSON files are read as structured data payloads.
   - Image files are decoded and rendered as visual assets.
6. The browser builds the page using the parsed HTML, applies the stylesheet, and renders the final layout to the user.

For a multi-page portfolio, this process repeats for each page load and for each linked asset. For example, when `index.html` loads, the browser may fetch the stylesheet, the profile image, and any other embedded assets. When the user navigates to `projects.html`, the browser loads that page and then separately requests the associated project images and CSS. This is a normal static asset-delivery model and is efficient because the browser does not need server-side processing to generate the page content.

### 3.2 The Role of MIME Types

MIME types are identifiers that describe the nature and format of a file being sent over HTTP. They are included in the response headers so that clients know how to interpret the content. MIME is essential because the browser must decide whether to parse a response as HTML, CSS, JSON, image, font, or another media type.

The key MIME types relevant to this project are:

- `text/html`: used for HTML pages such as `index.html`, `about.html`, `contact.html`, and others.
- `text/css`: used for stylesheet files like `assets/css/style.css`.
- `application/json`: used for the structured content file `data/data.json`.

The browser handles each one differently:

- For `text/html`, the browser parses the response as an HTML document, builds the DOM tree, and processes embedded links, forms, and semantic elements.
- For `text/css`, the browser interprets the body as CSS rules, applies them to the DOM, and updates the page appearance accordingly.
- For `application/json`, the browser treats the response as structured data. It can be consumed by scripts or stored for later processing, but it is not rendered as normal HTML markup.

If a MIME type mismatch occurs, the browser may not process the resource as intended. For example, if an HTML file is served with `text/plain` instead of `text/html`, the browser may display the raw file as text rather than rendering it as a page. If a CSS file is incorrectly served as `text/html`, the browser may try to parse it as markup and fail to apply styling. If JSON is served with the wrong MIME type or is interpreted as HTML, the client may not parse the data correctly, leading to broken dynamic logic or failed content loading. This is why correct server headers are critical for reliable rendering and correct browser behavior.

In summary, MIME types are the browser’s instruction manual for decoding server responses. Without the correct content type, the browser cannot reliably determine how the asset should be parsed and rendered. For a static portfolio like this one, correct MIME handling is essential to ensure that HTML pages render correctly, CSS styling applies, and JSON content remains usable as structured data.

## 4. CMS Comparative Evaluation

### 4.1 Architectural Trade-offs

A static XHTML/CSS/JSON architecture and a database-driven CMS such as WordPress represent two fundamentally different design paradigms. The static architecture used in this portfolio is pre-rendered and file-based, while a CMS is content-centric and database-backed. The trade-off is not simply one of preference but of system responsibility: static systems minimize runtime complexity, whereas CMS platforms centralize content management and publishing logic in a server-side application environment.

From a security standpoint, static pages have a significantly smaller attack surface. Because there is no server-side scripting layer, no database access layer, and no plugin execution environment, the system is less exposed to common exploitation vectors such as SQL injection, vulnerable plugins, or unauthorized admin actions. The portfolio is served as raw files, which eliminates the need for active back-end processing. This is a major advantage in a low-complexity academic portfolio where content is mostly informational and static.

In terms of speed, static delivery is often superior. A browser can request and render a small HTML file and a CSS stylesheet almost instantly, with minimal server overhead. Static hosting providers and simple file servers are extremely efficient because they do not need to query a database, process templates, or assemble pages dynamically. By contrast, a WordPress site generally requires PHP execution, database queries, template rendering, and plugin processing, all of which increase latency and server load.

Server overhead is therefore lower for the static portfolio. There is no application runtime, database engine, or content administration framework to maintain. This reduces maintenance complexity, hosting cost, and operational effort. A CMS, however, offers advantages in large-scale content operations where many editors and many content types are involved. In those scenarios, server overhead becomes a justifiable trade-off for convenience and scale.

Customizability, in a static portfolio, is strongest at the code level. Designers and developers have complete control over structure, semantics, styles, and deployment logic. Every page is explicit; there are no hidden template rules or theme constraints. This allows a highly bespoke portfolio experience. Yet customizability in a CMS is broader from an editorial standpoint: administrators can create pages, update posts, and manage content without editing files directly. The trade-off is that CMS customizability is often mediated by themes, plugins, and database architecture rather than direct source-code control.

### 4.2 Technical Defence of Migration

A migration to a full CMS would be justified only when the static portfolio evolves beyond the boundaries of a personal showcase into a more operational digital publishing platform. Three parameters are decisive.

#### 1. Team Size

If the portfolio expands from a single developer’s output into a multi-department or cross-functional environment, the benefits of a CMS become substantial. A static portfolio is ideal for a solo engineer or a small academic team where content changes are infrequent and controlled by one maintainer. However, once marketing, administration, student affairs, and academic staff all need to contribute content, file-based editing becomes difficult to coordinate. A CMS provides role-based access, content review workflows, and centralized publishing. This capability is essential when multiple contributors must manage content in parallel without introducing markup errors or inconsistent design updates.

#### 2. Content Update Frequency

A daily-updated blog, news feed, or project portal requires a content workflow that static files do not naturally provide. In a static portfolio, every update requires editing files and redeploying them. This is manageable for a personal portfolio or occasional project additions, but it becomes inefficient for constantly evolving content. A CMS enables content scheduling, versioning, richer metadata, taxonomy, and efficient publishing pipelines. If the institution expects weekly or daily updates, a CMS becomes technically and operationally necessary.

#### 3. Non-Technical User Access

The most persuasive reason to migrate is non-technical administration. A static site requires HTML and CSS knowledge, file management skills, and an understanding of deployment. This is acceptable for a single developer but not for a business or institutional website where administrators are not technical users. A CMS enables non-technical personnel to publish articles, upload media, and update content through a graphical interface. For institutional portfolios or academic portals, this lowers the skill barrier and reduces dependence on the original developer.

### 4.3 Conclusion

The current static portfolio is technically appropriate for a student engineering profile because it is lightweight, secure, fast, and easy to deploy. However, a migration to a CMS such as WordPress becomes justified when the project requires collaborative editing, frequent content publishing, and non-technical administration. In other words, the static architecture remains optimal for a personal or academic showcase, while a CMS becomes optimal once the website evolves into a real publishing system rather than a fixed portfolio artifact.

---

### Code Example: JSON-LD Metadata

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Person",
  "name": "Jimrah Peter Jimrah",
  "jobTitle": "Computer Engineering Student",
  "description": "Final-year Computer Engineering student at Ahmadu Bello University, Zaria.",
  "fieldOfStudy": "Computer Engineering",
  "affiliation": {
    "@type": "CollegeOrUniversity",
    "name": "Ahmadu Bello University, Zaria"
  },
  "sameAs": [
    "https://www.linkedin.com/in/jimrah-p-852a46129"
  ]
}
</script>
```

### Code Example: JSON Content Schema

```json
{
  "projects": [
    {
      "id": 1,
      "title": "Autonomous Delivery Robot",
      "date": "Current",
      "category": "Robotics",
      "description": "An Arduino-based indoor delivery robot with two trays, obstacle avoidance, and a Bluetooth-controlled mobile app.",
      "image_url": "assets/images/delivery-robot.jpg"
    }
  ],
  "education": [
    {
      "id": 1,
      "institution": "Ahmadu Bello University, Zaria",
      "start_date": "2020-01",
      "end_date": "2026-10",
      "qualification": "Bachelor of Engineering in Computer Engineering",
      "description": "Final-year student currently building an autonomous delivery robot."
    }
  ]
}
```

This final section confirms that the manual static architecture is not inferior in principle; it is simply best suited to a controlled, modest, and technically authoritative portfolio. It delivers performance, security, and clarity, while a CMS becomes strategically valuable only when editorial complexity and team-based content operations exceed the project’s current scope.
