# Educational Markdown Formatting Prompt

Use this prompt to ensure consistent, professional formatting for educational content in markdown files.

## General Formatting Rules

### Headers and Structure
- Use proper header hierarchy: `#`, `##`, `###` for main sections, subsections, and sub-subsections
- Include clear section breaks with appropriate spacing
- Use descriptive, concise header titles

### Mathematical Notation
- **Use LaTeX dollar sign notation** for all mathematical expressions: `$expression$` for inline math, `$$expression$$` for display math
- **Never use backticks** for mathematical expressions (avoid `` `expression` ``)
- **Use underscores for subscripts**: `$N_0$`, `$T_N$`, `$a_i$` (not Unicode subscripts like `$N₀$`)
- **Use proper LaTeX symbols**: 
  - `$\times$` for multiplication (not `x` or `*`)
  - `$\lg$` for logarithm base 2
  - `$\log$` for general logarithm
  - `$\sim$` for asymptotic notation
  - `$\Omega$`, `$\Theta$`, `$O$` for complexity notation
- **Use proper fraction notation**: `$N^3/6$` or `$\frac{N^3}{6}$`

### Text Formatting
- Use **bold** for emphasis on important terms and concepts
- Use *italics* for definitions, foreign terms, or subtle emphasis
- Use `backticks` for code elements, function names, variable names, and file names
- Use proper quotation marks and punctuation

### Lists and Structure
- Use consistent bullet points or numbered lists
- Maintain proper indentation for nested lists
- Ensure parallel structure in list items

### Code and Technical Elements
- Format code blocks with proper language specification:
  ```language
  code here
  ```
- Use `backticks` for inline code elements
- Format algorithm names, function names, and technical terms consistently

### Q&A Section Formatting
- Use **bold** for questions: `**Hỏi:**` or `**Question:**`
- Use **bold** for answers: `**Đáp:**` or `**Answer:**`
- Maintain consistent spacing between Q&A pairs
- Ensure mathematical expressions in Q&A follow the same LaTeX notation rules

### Language-Specific Considerations
- For Vietnamese content:
  - Use proper Vietnamese diacritics and punctuation
  - Maintain consistent terminology throughout
  - Follow Vietnamese grammar and syntax rules
- For English content:
  - Use consistent technical terminology
  - Follow standard academic writing conventions

### Mathematical Expression Examples
✅ **Correct:**
- `$f(N) = O(g(N))$`
- `$N_0$`, `$T_N$`, `$a_i$`
- `$N^3/6 - N^2/2 + N/3$`
- `$\sim N^3/2$`
- `$c \times g(N)$`

❌ **Incorrect:**
- `` `f(N) = O(g(N))` ``
- `$N₀$`, `$T₁$`, `$aᵢ$` (Unicode subscripts)
- `N^3/6 - N^2/2 + N/3` (no math formatting)
- `~N^3/2` (no math formatting)
- `c * g(N)` (asterisk instead of ×)

### Content Organization
- Start with clear introduction and context
- Use logical flow from basic to advanced concepts
- Include examples and illustrations where appropriate
- End sections with summary or key takeaways
- Use consistent terminology throughout the document

### Final Quality Checks
1. All mathematical expressions use LaTeX dollar sign notation
2. All subscripts use underscore format (`_`) not Unicode
3. Code elements use backticks, not dollar signs
4. Headers follow proper hierarchy
5. Q&A sections are consistently formatted
6. No mixing of mathematical notation styles
7. Proper spacing and paragraph breaks
8. Consistent terminology and language usage

## Usage Instructions
When applying these formatting rules:
1. Read through the entire document first
2. Identify all mathematical expressions and convert to LaTeX notation
3. Standardize all subscripts to underscore format
4. Format all code elements with backticks
5. Ensure Q&A sections follow the bold question/answer format
6. Check for consistent header hierarchy
7. Verify proper spacing and structure
8. Proofread for language consistency and accuracy

This prompt ensures professional, consistent formatting suitable for educational materials in computer science, algorithms, and mathematical content.
