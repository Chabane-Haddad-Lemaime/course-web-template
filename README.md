# Course Website Template

A [Jekyll](https://jekyllrb.com/) theme and template for building a course website. Easily customizable via YAML data files — no HTML editing required for most common changes.

## What's Included

- **Home page** – course description, goals, textbooks, and staff
- **Modules** – weekly or topic-based course modules
- **Outcomes** – course learning outcomes
- **Experiences** – hands-on lab or project pages
- **Readings** – assigned reading pages
- Multiple **color themes** based on [Flat UI Colors](http://flatuicolors.com/)

## Quick Start

### Prerequisites

- [Ruby](https://www.ruby-lang.org/) and [Bundler](https://bundler.io/)
- [Jekyll](https://jekyllrb.com/) 3.4+

### Run Locally

```bash
bundle install
bundle exec jekyll serve
```

Then open `http://localhost:4000` in your browser.

## Configuration

### 1. Site Settings (`_config.yml`)

Update the `baseurl` and `url` to match your deployment:

```yaml
baseurl: "/your-repo-name"
url: "https://your-username.github.io"
```

Choose a color theme:

```yaml
theme_color: silver   # silver | gold | midnight | green | turquoise | blue | purple | orange | red
```

### 2. Course Info (`_data/course_info.yml`)

```yaml
school: Your School Name
name: Course Name
number: ABC123
semester: Fall 2024
course_description: >
  A brief description of your course.
```

### 3. Course Outcomes (`_data/course_outcomes.yml`)

```yaml
-
  sort-order: 1
  id: outcome-1
  text: "Students will be able to..."
```

### 4. Textbooks (`_data/textbooks.yml`)

```yaml
-
  sort-order: 1
  title: Book Title
  edition: 4th
  authors:
    - Author Name
  isbn: 12345-67890
  required: true
  description: "Main textbook for the course."
```

### 5. Instructors (`_data/instructors.yml`)

```yaml
-
  sort-order: 1
  name: Instructor Name
  img_url: "https://example.com/photo.jpg"
  email: instructor@university.edu
  office_location: Building 1, Room 101
  office_hours:
    - Mon 1–3PM
    - Wed 3–5PM
```

### 6. Teaching Assistants (`_data/student_instructors.yml`)

Same structure as `instructors.yml`. Leave this file empty or remove entries to hide the section entirely.

## Deploying to GitHub Pages

1. Push this repository to GitHub.
2. In your repository settings, enable **GitHub Pages** using the `main` branch.
3. Make sure `baseurl` in `_config.yml` matches your repository name (e.g., `/course-web-template`).

## License

This template is open source and free to use for educational purposes.
