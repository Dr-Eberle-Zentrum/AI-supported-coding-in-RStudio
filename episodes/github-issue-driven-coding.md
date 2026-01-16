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

![](ai-mode-3.png)


GitHub issue-driven coding combines the structured approach of issue tracking 
with the power of AI-assisted development. 
By linking your coding work to specific GitHub issues, 
you create a clear workflow that helps both human collaborators 
and AI assistants understand the context and goals of your code changes.

This approach is particularly valuable when working with GitHub Copilot, 
as it provides the AI with rich context about what you're trying to accomplish, 
leading to more relevant and accurate suggestions.

Furthermore, you can "employ" the AI as additional team members,
assigning them specific issues to work on in parallel with your own tasks.
That way, you can leverage AI to accelerate development 
while focusing your efforts on reviewing the AI's solutions
and the more critical or complex parts of the project.

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

## How to Use GitHub Issues (with and without AI)

### Create a Detailed Issue

Before starting to code, create a GitHub issue that clearly describes:

1. **The problem or feature**: What needs to be done?
2. **Context**: Why is this needed?
3. **Requirements**: What are the specific technical requirements?
4. **Acceptance criteria**: How will you know it's done correctly?
5. **Examples**: Input/output examples if applicable

### Closing an Issue via Reference in Your Work

When referencing issues, include the issue number (with `#`) in your code or git workflow using the keywords "closes", "fixes", or "resolves",
GitHub will automatically link the commit to the issue and close it.

In the following, some examples of referencing issues are provided:

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

### Using Issues as AI Context for Autocompletion While Coding

When writing code that addresses an issue:

1. **Keep the issue open** in your browser
2. **Reference requirements** in code comments (maybe also the github repo's URL)
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

### Triggering Autonomous AI Coding via Issues

When you create a detailed GitHub issue, you can "assign" it to GitHub Copilot 
(if supported in your environment) or simply reference it while coding.

This will trigger the following workflow:

1. GitHub Copilot reads the issue description
2. It creates a new git branch for the issue
3. It generates code that addresses the issue requirements within the branch
4. It creates a pull request for review and lists all changes made
5. It will send you a notification to review the PR
6. You will review the code, request changes if necessary, and merge it when satisfied

That way, the AI can work semi-autonomously on well-defined tasks, freeing you to focus on higher-level design and review.

This approach works very well for

- Specific feature implementations
- Bug fixes
- Error identification and handling
- Code refactoring
- Documentation generation or improvement/update
- Test case creation
- And more...


## GitHub Repositories vs. RStudio Projects

While GitHub repositories and RStudio projects are related, they serve different purposes in the development workflow.

- **GitHub Repository**: A GitHub repository is a remote storage space on GitHub where your project's files, including code, documentation, and version history, are hosted. It allows for collaboration, issue tracking, and version control using Git.
- **RStudio Project**: An RStudio project is a local environment within RStudio that organizes your work. It includes settings, file paths, and configurations specific to your R development. An RStudio project can be linked to a GitHub repository for version control and collaboration.

When working with issue-driven coding, you typically create and manage issues on the GitHub repository, while you do the actual coding and testing within your local RStudio project.

Thus, you have to ensure that your RStudio project is connected to the corresponding GitHub repository and you synchronize changes between them using Git commands.

### GitHub Authentication in RStudio

In order to enable the communication between your local RStudio and the online GitHub server, you need to authenticate RStudio with your GitHub account.
This can be done by generating a Personal Access Token (PAT) on GitHub and configuring RStudio to use it for authentication.

For detailed instructions on how to set this up, refer to the respective section in [Happy Git and GitHub for the useR](https://happygitwithr.com/https-pat).

A general description about the integration of versioning systems like git in RStudio can be found in the [RStudio User Guide](https://docs.posit.co/ide/user/ide/guide/tools/version-control.html).

### Starting an RStudio project from a GitHub repository

Once your authentication is set up, you can clone a GitHub repository directly into RStudio to create a new project.

To this end

1. Open RStudio
2. Go to `File` -> `New Project...`
3. Select `Version Control`
4. Choose `Git`
5. Enter the repository URL from GitHub
   - Note: ensure you use the "https://..." URL format if using PAT authentication!
6. Select the local directory where you want to store the project
7. Click `Create Project`

Afterwards, RStudio will create a new project linked to the GitHub repository, allowing you to work on the code locally while managing issues and version control through GitHub.

Within the project you can use the Git tab in RStudio to commit changes, push updates to GitHub, and pull the latest changes from the repository.

::::::::::::::::::::: callout

## Best Practices for git-based Projects

- always ensure that you pull the latest changes from GitHub before starting new work to avoid merge conflicts.
  - thus, do a "pull" whenever you open RStudio to work on the project
- commit changes frequently with clear messages that reference relevant issue numbers
- don't forget to "push" your commits to GitHub to keep the remote repository updated

When using with GitHub issues, ensure that your commit messages and pull requests clearly reference the issues they address.

When **using GitHub Copilot for issue-driven coding**, always review the generated code carefully to ensure it meets the issue requirements before merging it into the main branch.

- ensure your remote repository is up-to-date before starting work on an issue..
  - check if you **PUSH**ed all your local changes to GitHub
- assign the issue to GitHub Copilot (if supported)
  - review and merge the respective pull request if satisfied
- **PULL** these changes into your local RStudio project to keep it synchronized !!!


::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints 

- Issue-driven development provides structure and context for AI-assisted coding
- Detailed issues with clear requirements help AI assistants generate better code
- Reference issue numbers in commits, comments, and code to maintain traceability
- Use issues to guide Copilot for autonomous code generation and review
- Effective use of GitHub repositories and RStudio projects enhances collaboration and version control
- **If not familiar with `git`, read ["Happy Git and GitHub for the useR"](https://happygitwithr.com/) for a gentle introduction**

::::::::::::::::::::::::::::::::::::::::::::::::
