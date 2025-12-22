---
title: "GitHub Issue-Driven Coding with Copilot"
teaching: 25
exercises: 15
---

:::::::::::::::::::::::::::::::::::::: questions 

- What is GitHub issue-driven coding with Copilot?
- How can I use GitHub issues to guide AI-assisted development?
- What are the best practices for working with Copilot on GitHub issues?
- How do I effectively communicate tasks to Copilot through issues?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Understand the concept of issue-driven development with AI assistance
- Learn how to structure GitHub issues for effective AI collaboration
- Master techniques for guiding Copilot through issue-based workflows
- Apply best practices for iterative development with issue tracking
- Recognize when to use issue-driven AI assistance vs. direct coding

::::::::::::::::::::::::::::::::::::::::::::::::

## Using AI autonomously

![Autonomous AI usage](ai-mode-3.png)


GitHub issue-driven coding combines the structured approach of issue tracking with the power of AI-assisted development. By linking your coding work to specific GitHub issues, you create a clear workflow that helps both human collaborators and AI assistants understand the context and goals of your code changes.

This approach is particularly valuable when working with GitHub Copilot, as it provides the AI with rich context about what you're trying to accomplish, leading to more relevant and accurate suggestions.

## What is Issue-Driven Coding?

Issue-driven coding is a development practice where:

1. **Tasks are defined as issues**: Each feature, bug fix, or improvement starts as a GitHub issue
2. **Issues provide context**: The issue description explains the problem, requirements, and acceptance criteria
3. **Code references issues**: Commits and pull requests link back to the issues they address
4. **Progress is tracked**: Issue status reflects the current state of development

::::::::::::::::::::::::::::::::::::: callout

### Why Combine Issues with AI Assistance?

When you work on code while referencing a GitHub issue, AI assistants like Copilot can:
- Better understand the task context
- Generate code that aligns with the stated requirements
- Suggest implementations that match the issue's acceptance criteria
- Help maintain consistency across related changes
- Enable parallelizing progress on multiple subtasks when issues are well-defined

::::::::::::::::::::::::::::::::::::::::::::::::

## Use Cases for Issue-Driven AI Coding

### 1. Feature Implementation

**Scenario**: You need to add a new feature to analyze data trends.

**GitHub Issue Example**:
```markdown
Title: Add trend analysis function to data processing module

Description:
Create a function that calculates linear trends in time series data.

Requirements:
- Accept a data frame with date and value columns
- Calculate slope and intercept using linear regression
- Return results as a named list
- Handle missing values appropriately
- Include error handling for invalid inputs

Acceptance Criteria:
- Function works with sample dataset
- Returns correct statistical values
- Handles edge cases (empty data, all NAs, single point)
```

**Using Copilot**: When you reference this issue while coding, Copilot understands you need a robust statistical function and will suggest implementations that include error handling and edge case management.

### 2. Bug Fixes

**Scenario**: Users report incorrect calculations in your analysis code.

**GitHub Issue Example**:
```markdown
Title: Fix mean calculation ignoring NA values

Description:
The calculate_statistics() function returns NA when any value 
in the input is NA, instead of computing the mean of available values.

Steps to Reproduce:
1. Call calculate_statistics(c(1, 2, NA, 4))
2. Expected: mean should be 2.33 (mean of 1, 2, 4)
3. Actual: function returns NA

Expected Behavior:
Function should use na.rm = TRUE by default or provide an option 
to handle NA values.
```

**Using Copilot**: With this context, Copilot will suggest fixes that specifically address NA handling, such as adding `na.rm = TRUE` parameters.

### 3. Code Refactoring

**Scenario**: You need to improve code performance or readability.

**GitHub Issue Example**:
```markdown
Title: Refactor data loading functions for better performance

Description:
Current data loading is slow with large files. Refactor to use 
more efficient approaches.

Current Problems:
- Uses loops to process rows individually
- Reads entire file into memory at once
- No progress indication for large files

Proposed Improvements:
- Use vectorized operations where possible
- Implement chunked reading for large files
- Add optional progress bar
- Maintain backward compatibility
```

**Using Copilot**: The AI will suggest vectorized alternatives and modern R idioms that address the performance concerns.

### 4. Adding Tests

**Scenario**: You need to add test coverage for existing functions.

**GitHub Issue Example**:
```markdown
Title: Add unit tests for data validation functions

Description:
Add comprehensive tests for validate_input() and sanitize_data() 
functions.

Test Coverage Needed:
- Valid input handling
- Invalid input rejection
- Edge cases (empty data, single value, extreme values)
- Type checking
- NA and NULL handling

Framework: Use testthat
Target Coverage: 90%+
```

**Using Copilot**: The AI will generate appropriate test cases using the testthat framework that cover the specified scenarios.

::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 1: Create an Issue for AI-Assisted Development

Write a GitHub issue for adding a data visualization function to your R project. Include:
- Clear title
- Detailed description
- Specific requirements
- Acceptance criteria

Think about what information would help an AI assistant generate appropriate code.

:::::::::::::::::::::::: solution 

## Example Solution

```markdown
Title: Create scatter plot function with trend line for correlation analysis

Description:
Implement a function to create scatter plots with optional trend lines 
for exploring relationships between variables.

Requirements:
- Function name: plot_correlation()
- Parameters:
  - data: data frame
  - x_var: name of x-axis variable
  - y_var: name of y-axis variable
  - add_trend: logical, whether to add trend line (default: TRUE)
  - title: optional plot title
- Use ggplot2 for plotting
- Include correlation coefficient in plot subtitle when trend is shown
- Return a ggplot object for further customization

Acceptance Criteria:
- Creates clear, readable scatter plot
- Trend line uses appropriate statistical method (lm)
- Handles data with missing values
- Includes proper axis labels and title
- Works with sample mtcars dataset

Example Usage:
plot_correlation(mtcars, "wt", "mpg", title = "Weight vs MPG")
```

This issue provides clear context that helps Copilot suggest appropriate ggplot2 code with statistical elements.

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

## How to Use GitHub Issues with Copilot

### Step 1: Create a Detailed Issue

Before starting to code, create a GitHub issue that clearly describes:

1. **The problem or feature**: What needs to be done?
2. **Context**: Why is this needed?
3. **Requirements**: What are the specific technical requirements?
4. **Acceptance criteria**: How will you know it's done correctly?
5. **Examples**: Input/output examples if applicable

### Step 2: Reference the Issue in Your Work

**In commit messages**:
```bash
git commit -m "Add trend analysis function #42"
git commit -m "Fix NA handling in statistics - fixes #38"
```

**In code comments**:
```r
# Implementation for GitHub issue #42: Add trend analysis
# See: https://github.com/username/repo/issues/42
analyze_trend <- function(data, date_col, value_col) {
  # Function implementation
}
```

**In pull request descriptions**:
```markdown
Closes #42

This PR implements the trend analysis function as specified in the issue.

Changes:
- Added analyze_trend() function
- Included error handling for edge cases
- Added unit tests for validation
```

### Step 3: Use Issue Context While Coding

When writing code that addresses an issue:

1. **Keep the issue open** in your browser
2. **Reference requirements** in code comments
3. **Write descriptive comments** that mirror the issue's language
4. **Test against acceptance criteria** listed in the issue

**Example workflow**:

```r
# GitHub Issue #42: Add trend analysis function
# Requirement: Accept data frame with date and value columns
# Requirement: Calculate slope and intercept using linear regression
# Requirement: Handle missing values appropriately

analyze_trend <- function(data, date_col = "date", value_col = "value") {
  # Input validation (Requirement: error handling for invalid inputs)
  if (!is.data.frame(data)) {
    stop("Input must be a data frame")
  }
  
  # Copilot will suggest implementations based on the comments
  # and your typing that align with the requirements
}
```

### Step 4: Leverage Copilot's Context Understanding

GitHub Copilot can access:
- **Open files in your editor**: Related code that provides context
- **Your comments**: Especially comments that reference requirements
- **Function and variable names**: Descriptive names guide suggestions
- **Your typing patterns**: The direction you're heading

::::::::::::::::::::::::::::::::::::: callout

### Maximizing Copilot's Effectiveness

Write comments that:
- Reference the issue number
- Use exact wording from the issue requirements
- Break down complex tasks into steps
- Specify data types and expected behavior

Example:
```r
# Issue #42 requirement: calculate slope and intercept using linear regression
# Input: data frame with numeric date and value columns
# Output: named list with 'slope' and 'intercept' values
# Handle: Remove rows with NA in either column before analysis
```

This gives Copilot clear, specific context for generating appropriate code.

::::::::::::::::::::::::::::::::::::::::::::::::

## Best Practices for Issue-Driven AI Coding

### 1. Write Specific, Actionable Issues

**Good Issue**:
```markdown
Title: Add parameter validation to process_data function

Description:
The process_data() function currently doesn't validate inputs,
causing cryptic errors when users pass invalid data.

Add validation for:
- data must be a data frame
- required columns: 'id', 'value', 'timestamp'
- 'value' must be numeric
- 'timestamp' must be Date or POSIXct

Return informative error messages that guide users to fix the problem.
```

**Less Effective Issue**:
```markdown
Title: Improve process_data

Description: Make it better
```

### 2. Include Examples in Issues

Examples help both humans and AI understand requirements:

```markdown
Expected Behavior:
```r
# Valid input
data <- data.frame(
  id = 1:3,
  value = c(10.5, 20.3, 15.7),
  timestamp = as.Date(c("2024-01-01", "2024-01-02", "2024-01-03"))
)
result <- process_data(data)  # Should succeed

# Invalid input
bad_data <- data.frame(x = 1:3, y = 4:6)
process_data(bad_data)  # Should give clear error about missing columns
```
```

### 3. Break Down Complex Tasks

Instead of one large issue, create multiple related issues:

**Parent Issue**: "Implement data export functionality"
- Issue #45: Add CSV export function
- Issue #46: Add Excel export function  
- Issue #47: Add export format validation
- Issue #48: Add unit tests for export functions

This gives you:
- Clearer focus for each coding session
- Better AI context for specific subtasks
- Easier progress tracking
- More manageable pull requests

### 4. Keep Issues Updated

As you work, update the issue with:
- Progress notes
- Discoveries or changes in approach
- Questions or blockers
- Links to related commits or PRs

This maintains context for later work and helps team members (and AI) understand the evolution of the solution.

### 5. Use Issue Templates

Create issue templates for common scenarios:

**Feature Request Template**:
```markdown
## Feature Description
[Clear description of the feature]

## Use Case
[Why is this needed? Who will use it?]

## Requirements
- [ ] Requirement 1
- [ ] Requirement 2

## Acceptance Criteria
- [ ] Criterion 1
- [ ] Criterion 2

## Implementation Notes
[Any technical considerations]
```

::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 2: Issue-Driven Development Workflow

You have an existing function that needs improvement:

```r
calc <- function(x, y) {
  x + y * 2
}
```

Users report it's unclear what this function does and it doesn't handle errors.

1. Write a GitHub issue describing the problems and improvements needed
2. Write code comments referencing the issue
3. How would you structure your commits?

:::::::::::::::::::::::: solution 

## Solution

**GitHub Issue**:
```markdown
Title: Improve calc() function documentation and error handling

Description:
The calc() function has unclear purpose and lacks input validation.

Current Problems:
- Unclear function name and purpose
- No documentation
- No parameter validation
- No error messages for invalid inputs

Improvements Needed:
1. Rename to descriptive name (e.g., calculate_adjusted_sum)
2. Add roxygen2 documentation
3. Add parameter validation (must be numeric)
4. Add informative error messages
5. Include usage examples

Acceptance Criteria:
- Function has clear, descriptive name
- Complete roxygen2 documentation with examples
- Validates that inputs are numeric
- Returns helpful error messages for invalid inputs
```

**Code with comments**:
```r
# Issue #50: Improve calc() documentation and error handling
# Renamed from calc() to calculate_adjusted_sum() for clarity

#' Calculate adjusted sum with weighted second parameter
#'
#' Computes x + (y * 2), useful for calculating adjusted totals
#' where the second parameter has double weight.
#'
#' @param x Numeric value or vector for base amount
#' @param y Numeric value or vector for weighted amount
#' @return Numeric value or vector of adjusted sums
#' @examples
#' calculate_adjusted_sum(10, 5)  # Returns 20
#' calculate_adjusted_sum(c(1,2), c(3,4))  # Returns c(7, 10)
#' @export
calculate_adjusted_sum <- function(x, y) {
  # Issue #50 requirement: validate inputs are numeric
  if (!is.numeric(x)) {
    stop("Parameter 'x' must be numeric, got ", class(x)[1])
  }
  if (!is.numeric(y)) {
    stop("Parameter 'y' must be numeric, got ", class(y)[1])
  }
  
  # Issue #50: Original calculation preserved, now with clear purpose
  x + y * 2
}
```

**Commit structure**:
```bash
# Commit 1: Rename function
git commit -m "Rename calc to calculate_adjusted_sum for clarity (#50)"

# Commit 2: Add documentation
git commit -m "Add roxygen2 documentation to calculate_adjusted_sum (#50)"

# Commit 3: Add validation
git commit -m "Add input validation and error messages (#50)"

# Commit 4: Add tests
git commit -m "Add unit tests for calculate_adjusted_sum (#50)"
```

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

## Guiding and Triggering Changes with Issues

### Technique 1: Use Issue Labels for Context

Labels help categorize work and can guide your AI-assisted development:

- `enhancement`: Feature additions
- `bug`: Bug fixes
- `refactoring`: Code improvements without behavior changes
- `documentation`: Documentation updates
- `testing`: Test additions or fixes
- `performance`: Performance optimizations

When working on an issue with specific labels, mention the label in your comments:

```r
# Bug fix for issue #52 (labeled: bug, NA-handling)
# Ensure mean calculation handles NA values correctly
calculate_mean <- function(x, na.rm = TRUE) {
  mean(x, na.rm = na.rm)
}
```

### Technique 2: Progressive Enhancement with Issues

Create a series of related issues for iterative development:

**Issue #60**: Basic implementation
**Issue #61**: Add error handling  
**Issue #62**: Optimize performance
**Issue #63**: Add comprehensive tests
**Issue #64**: Improve documentation

Work through them sequentially, with each issue building on the previous work.

### Technique 3: Use Issue Checklists

Within an issue, use checklists to track subtasks:

```markdown
## Implementation Checklist

- [ ] Create main function structure
- [ ] Add input validation
- [ ] Implement core logic
- [ ] Add error handling
- [ ] Write unit tests
- [ ] Add documentation
- [ ] Test with real data
```

Reference specific checklist items in your commits:

```bash
git commit -m "Add input validation for issue #65 (checklist item 2)"
```

### Technique 4: Link Related Issues

Create a network of related issues:

```markdown
Part of #70 (parent issue: Data export improvements)
Related to #68 (CSV format handling)
Blocks #72 (export UI implementation)
```

This helps maintain context across a larger feature or project.

::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 3: Multi-Issue Workflow

You're adding a new data analysis pipeline. Plan the issues needed:

Requirements:
- Load data from multiple file formats (CSV, Excel, RDS)
- Validate data structure and types
- Clean data (remove duplicates, handle missing values)
- Perform statistical analysis
- Generate report with visualizations
- Export results

Create an issue structure with:
1. A parent tracking issue
2. Individual implementation issues
3. Labels for each issue
4. Dependencies between issues

:::::::::::::::::::::::: solution 

## Solution

**Parent Issue #80**:
```markdown
Title: Implement Complete Data Analysis Pipeline
Labels: enhancement, epic

Description:
Create end-to-end data analysis pipeline from loading to reporting.

Sub-Issues:
- #81: Add multi-format data loading
- #82: Implement data validation
- #83: Add data cleaning functions
- #84: Create statistical analysis module
- #85: Build report generation with visualizations
- #86: Add results export functionality
- #87: Write integration tests for complete pipeline

Dependencies:
- #82 depends on #81
- #83 depends on #82
- #84 depends on #83
- #85 depends on #84
- #86 depends on #85
- #87 depends on all others
```

**Issue #81**:
```markdown
Title: Add multi-format data loading support
Labels: enhancement, data-loading
Part of: #80

Description:
Create functions to load data from CSV, Excel, and RDS formats.

Requirements:
- Function: load_data(filepath, format)
- Auto-detect format from extension if not specified
- Consistent output format (data frame)
- Error handling for missing files or corrupt data
```

**Issue #82**:
```markdown
Title: Implement data structure validation
Labels: enhancement, validation
Part of: #80
Depends on: #81

Description:
Validate loaded data has expected structure and types.

Requirements:
- Function: validate_data(data, schema)
- Check required columns exist
- Validate column types
- Check value ranges
- Return detailed validation report
```

Continue this pattern for remaining issues #83-#87.

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

## Advanced Tips for Issue-Driven AI Coding

### 1. Reference Issues in Code Structure

```r
# Issue #90: Data Pipeline Module
# This module implements the data loading and validation pipeline

#' @name data_pipeline
#' @title Data Pipeline Functions
#' @description Functions for loading, validating, and processing data
#'              Implements requirements from GitHub issue #90
NULL

# Issue #91: Load data from file
#' @rdname data_pipeline
load_data <- function(filepath) {
  # Implementation
}

# Issue #92: Validate data structure
#' @rdname data_pipeline
validate_data <- function(data, schema) {
  # Implementation
}
```

### 2. Use Issue Milestones

Group related issues into milestones:
- **Milestone**: "Version 2.0 - Enhanced Analysis Features"
  - Issue #100: Add advanced statistics
  - Issue #101: Implement machine learning models
  - Issue #102: Create interactive visualizations

This provides higher-level context for your development work.

### 3. Automate Issue References

Use Git hooks or GitHub Actions to automatically:
- Link commits to issues
- Update issue status when branches are merged
- Generate changelogs from issue titles
- Notify stakeholders of progress

### 4. Document Decisions in Issues

When you make important technical decisions, document them in the issue:

```markdown
## Implementation Decision

After testing both approaches, choosing data.table over dplyr for this 
function because:
- 10x faster with large datasets in benchmarks
- Lower memory usage
- Syntax acceptable for this use case

Benchmark results: [link to gist]
```

This helps future developers (and AI assistants) understand why code is structured a certain way.

### 5. Create "Good First Issue" Labels

For simpler tasks that benefit from AI assistance:

```markdown
Label: good-first-issue, AI-friendly

Title: Add input validation to format_output function

Description:
Simple addition of parameter checks to existing function.
Clear requirements, good for practicing AI-assisted development.

Requirements:
- Check that input is a data frame
- Verify required columns exist
- Validate format parameter is one of: "table", "json", "csv"
```

## When to Use Issue-Driven Development

### Good Use Cases

✅ **Feature development**: Clear requirements and acceptance criteria
✅ **Bug fixes**: Reproducible problems with expected behavior
✅ **Refactoring**: Specific improvements to existing code
✅ **Testing**: Adding test coverage to existing functions
✅ **Documentation**: Improving code documentation and examples

### Less Suitable Cases

❌ **Exploratory coding**: When you're still figuring out what's needed
❌ **Very small changes**: Single-line typo fixes
❌ **Rapid prototyping**: Quick experiments and throwaway code
❌ **Emergency hotfixes**: Critical fixes that need immediate deployment

::::::::::::::::::::::::::::::::::::: callout

### Balancing Structure and Flexibility

Issue-driven development provides structure, but don't let it slow you down:
- Create lightweight issues for tracking, not bureaucracy
- It's OK to discover new requirements during implementation
- Update issues as understanding evolves
- Close or merge issues that become redundant

::::::::::::::::::::::::::::::::::::::::::::::::

## Common Pitfalls and How to Avoid Them

### Pitfall 1: Issues Too Vague

**Problem**: "Make the code better"
**Solution**: Specify what "better" means:
- Faster? (Provide benchmark targets)
- More readable? (Specify style guidelines)
- More robust? (List edge cases to handle)

### Pitfall 2: Issues Too Detailed

**Problem**: Issue contains complete implementation code
**Solution**: Describe requirements and constraints, not implementation. Let AI and developer judgment determine the best approach.

### Pitfall 3: Not Updating Issues

**Problem**: Issue doesn't reflect current understanding or progress
**Solution**: Edit issues as you learn. Add comments about discoveries, blockers, or approach changes.

### Pitfall 4: Ignoring Issue Context While Coding

**Problem**: Writing code without referencing the issue's requirements
**Solution**: Keep the issue open in your browser. Reference it in comments. Check off requirements as you implement them.

### Pitfall 5: Over-Relying on AI

**Problem**: Accepting all AI suggestions without validation
**Solution**: Use issues to define test cases. Verify AI-generated code meets all requirements before committing.

::::::::::::::::::::::::::::::::::::: discussion

### Group Discussion

Discuss with your peers:
- How do you currently track development tasks?
- What information do you typically include in issues?
- How might issue-driven development change your workflow?
- What challenges do you anticipate in adopting this approach?
- How can AI assistance complement issue tracking in your projects?

:::::::::::::::::::::::::::::::::::::::::::::::::::

## Practical Workflow Summary

1. **Plan**: Create detailed issue with requirements and acceptance criteria
2. **Reference**: Include issue number in branch name, commits, and code comments  
3. **Context**: Keep issue open while coding; let it guide your work
4. **Guide AI**: Write comments that mirror issue requirements to guide Copilot
5. **Test**: Verify implementation meets issue's acceptance criteria
6. **Update**: Keep issue updated with progress and discoveries
7. **Close**: Link PR to issue; ensure all requirements are met

## Tools and Integrations

### GitHub CLI

```bash
# Create issue from command line
gh issue create --title "Add data export feature" --body "Requirements..."

# List issues
gh issue list --label enhancement

# View issue details
gh issue view 42
```

### RStudio Integration

- Keep GitHub open in browser alongside RStudio
- Reference issue numbers in code comments
- Use descriptive branch names: `feature/42-add-export`

### VS Code Integration

- GitHub Pull Requests and Issues extension
- View and create issues without leaving editor
- Automatic issue linking in commit messages

::::::::::::::::::::::::::::::::::::: keypoints 

- Issue-driven development provides structure and context for AI-assisted coding
- Detailed issues with clear requirements help AI assistants generate better code
- Reference issue numbers in commits, comments, and code to maintain traceability
- Break complex tasks into multiple focused issues for better results
- Use issue descriptions and checklists to guide your coding workflow
- Keep issues updated to maintain accurate context for ongoing work
- Balance structure with flexibility; don't let process slow down development
- Test AI-generated code against issue requirements before committing
- Use issue labels, milestones, and dependencies to organize complex projects

::::::::::::::::::::::::::::::::::::::::::::::::
