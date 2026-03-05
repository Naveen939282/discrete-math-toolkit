# Discrete Math Toolkit – Partition & Equivalence Relation Visualizer

## 1. Project Overview

**Project Name:** Discrete Math Toolkit  
**Project Type:** Single-page web application (educational math tool)  
**Core Functionality:** Interactive tool for generating set partitions and visualizing equivalence classes based on divisibility relations  
**Target Users:** Math students, educators, and anyone learning discrete mathematics

---

## 2. UI/UX Specification

### Layout Structure

**Page Sections:**
- Header: App title with mathematical icon
- Main content: Two stacked cards (Partition Generator, Equivalence Class Generator)
- Footer: Project credits

**Layout:**
- Centered card layout with max-width 800px
- Cards have generous padding (40px desktop, 24px mobile)
- Vertical stacking with 32px gap between cards

**Responsive Breakpoints:**
- Mobile: < 640px (single column, reduced padding)
- Tablet: 640px - 1024px
- Desktop: > 1024px

### Visual Design

**Color Palette:**
- Background: `#0f0f1a` (deep navy-black)
- Card background: `rgba(255, 255, 255, 0.03)` with backdrop blur
- Card border: `rgba(255, 255, 255, 0.08)`
- Primary accent: `#00d4aa` (teal-mint)
- Secondary accent: `#7c3aed` (violet)
- Text primary: `#e8e8ed`
- Text secondary: `#8b8b9a`
- Error: `#ff6b6b`
- Success: `#00d4aa`

**Typography:**
- Font family: 'JetBrains Mono' for math outputs, 'Outfit' for UI text
- Headings: 700 weight, 1.5rem - 2rem
- Body: 400 weight, 1rem
- Math output: 500 weight, 1.1rem

**Spacing System:**
- Base unit: 8px
- Card padding: 40px
- Section gap: 32px
- Input gap: 16px

**Visual Effects:**
- Glassmorphism cards with `backdrop-filter: blur(20px)`
- Subtle box shadows with colored glow
- Smooth transitions (0.3s ease)
- Floating background orbs for atmosphere

### Components

**Input Fields:**
- Dark background `rgba(255, 255, 255, 0.05)`
- Border: 1px solid `rgba(255, 255, 255, 0.1)`
- Focus state: border-color transitions to primary accent
- Placeholder text in secondary color
- Rounded corners (12px)

**Buttons:**
- Primary: Gradient background (primary to secondary accent)
- Hover: Slight scale (1.02) and glow effect
- Active: Scale down (0.98)
- Disabled: Reduced opacity (0.5)

**Result Display:**
- Monospace font for mathematical output
- Card-style blocks for each partition/class
- Color-coded remainders in equivalence classes
- Smooth fade-in animation on results

**Toggle Switch (Dark Mode):**
- Pill-shaped toggle
- Smooth slide animation
- Sun/moon icons

---

## 3. Functionality Specification

### Feature 1: Partition Generator

**Input:**
- Text input field for elements (space-separated)
- Example valid inputs: "1 2 3" or "a b c d" or "1 2 3 4 5 6"

**Validation:**
- Non-empty input required
- Maximum 6 elements (performance constraint)
- Elements must be non-empty strings
- Show error message for invalid input

**Algorithm:**
- Recursive algorithm to generate all partitions
- Uses Bell numbers formula for count verification
- Returns array of partition arrays

**Output Display:**
- Total number of partitions (Bell number)
- Each partition as set of blocks
- Format: `{{1, 2}, {3}, {4}}` style

### Feature 2: Equivalence Class Generator

**Input:**
- Integer n (divisor) - required
- Range start (optional, default -20)
- Range end (optional, default 20)

**Validation:**
- n must be positive integer > 0
- Range must be valid (start < end)
- Range limited to prevent performance issues

**Algorithm:**
- For each number in range, calculate remainder: `num % n`
- Group numbers by remainder
- Display each equivalence class as [n] = {numbers}

**Output Display:**
- Mathematical notation: `a ≡ b (mod n)`
- Each class with its remainder
- Color-coded classes for visual distinction

### Feature 3: Dark Mode Toggle

- Toggle between light and dark themes
- Persists preference in localStorage
- Smooth transition between themes

### Feature 4: Download Results

- Button to download current results as .txt file
- Includes timestamp and section header
- Formatted as plain text

### Edge Cases

- Empty input → Show validation error
- More than 6 elements → Show limit warning
- Invalid numbers in range → Show error
- Zero or negative n for equivalence → Show error

---

## 4. Acceptance Criteria

### Visual Checkpoints
- [ ] Dark theme loads by default with proper colors
- [ ] Cards have glassmorphism effect visible
- [ ] All text is readable (proper contrast)
- [ ] Responsive layout works on mobile width
- [ ] Animations are smooth (no jank)
- [ ] Dark mode toggle works correctly

### Functional Checkpoints
- [ ] Partition: "1 2 3" returns 5 partitions (Bell(3) = 5)
- [ ] Partition: Shows all partitions correctly formatted
- [ ] Equivalence: n=3, range -5 to 5 gives classes: {-3, 0, 3}, {-2, 1, 4}, {-5, -1, 2}
- [ ] Input validation shows appropriate errors
- [ ] Download button creates valid text file
- [ ] Maximum 6 elements enforced

### Code Quality
- [ ] No external dependencies
- [ ] Clean modular JavaScript
- [ ] Well-commented algorithms
- [ ] No console errors on normal use

---

## 5. Technical Implementation Notes

### Partition Algorithm (Recursive)
```
function partitions(set):
  if set is empty: return [[]]
  if set has one element: return [[[element]]]
  
  first = set[0]
  rest = set[1:]
  
  partitionsOfRest = partitions(rest)
  
  result = []
  for each partition in partitionsOfRest:
    // Add singleton {first}
    result.push([[first]] + partition)
    // Add first to each existing block
    for each block in partition:
      newBlock = [first] + block
      newPartition = partition with block replaced by newBlock
      result.push(newPartition)
  
  return result
```

### Equivalence Class Algorithm
```
For each number x in [start, end]:
  remainder = x mod n (handle negative correctly)
  add x to class[remainder]

// JavaScript negative modulo fix:
// ((x % n) + n) % n
```

### File Structure
Single `index.html` file containing:
- Embedded CSS in `<style>` tag
- Embedded JavaScript in `<script>` tag
- Google Fonts loaded via CDN (with fallbacks)

