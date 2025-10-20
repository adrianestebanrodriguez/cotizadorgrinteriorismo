# GR Interiorismo Proposal Generator - AI Assistant Guide

## Project Overview
This is a web-based interior design proposal generator for GR Interiorismo. It's a single-page application that generates professionally formatted PDF proposals through browser printing.

### Key Technologies
- HTML5 for structure
- Tailwind CSS for styling (via CDN)
- Vanilla JavaScript for interactivity
- CSS Print Media Queries for PDF generation
- Inter font family from Google Fonts

## Core Architecture

### Component Structure
- Single index.html file containing all application logic
- Two main container divs:
  1. `#app-container`: Interactive form interface
  2. `#proposal-output`: Hidden PDF preview (visible only during print)

### Key Data Management
- Budget calculations are handled through the `calculateBudget()` function
- All form fields trigger `updateProposalOutput()` to sync PDF preview
- Dynamic budget items use event delegation for real-time updates

## Critical Patterns

### Print/Export Workflow
The PDF generation relies on CSS @media print rules that:
1. Hide the form interface (`#app-container`)
2. Show and format the proposal preview (`#proposal-output`)
3. Apply specific print styling (margins, colors, page breaks)

Example from styles:
```css
@media print {
    #app-container {
        display: none !important;
        visibility: hidden !important;
    }
    #proposal-output {
        display: block !important;
        visibility: visible !important;
        padding: 1.5cm !important;
    }
}
```

### Dynamic Budget Management
Budget items are managed through:
- `addLineItem(activity, value)` for creating new entries
- Event listeners on inputs for real-time calculation
- Centralized `calculateBudget()` for total computation
- IGIC (Canary Islands tax) rate constant: `IGIC_RATE = 0.07`

### Data Security
All user input is sanitized before rendering using:
- `escapeHTML()` for basic text
- `formatTextareaForDisplay()` for multiline content with line breaks

## Development Workflow

### Making Changes
1. Style changes should consider both screen and print media queries
2. New form fields must be:
   - Added to the form UI
   - Connected to the PDF generator via `updateProposalOutput()`
   - Sanitized before rendering
   - Styled for both screen and print

### Testing
Key test scenarios:
1. Form input validation
2. Budget calculations accuracy
3. PDF generation formatting
4. Print layout across different paper sizes

## Integration Points

### External Dependencies
- Tailwind CSS: `https://cdn.tailwindcss.com`
- Google Fonts (Inter): `fonts.googleapis.com/css2?family=Inter:wght@100..900`

### Browser Requirements
- Modern browser with CSS Grid support
- JavaScript enabled
- Print capability for PDF generation