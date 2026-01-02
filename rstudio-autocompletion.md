---
title: "RStudio Autocompletion with Copilot"
teaching: 25
exercises: 15
---

:::::::::::::::::::::::::::::::::::::: questions 

- How does GitHub Copilot work as an autocompletion tool in RStudio?
- What are the best practices for getting useful suggestions from Copilot?
- How can I accept, reject, or modify Copilot suggestions?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Understand how GitHub Copilot generates code suggestions
- Learn techniques for writing effective prompts
- Practice accepting, rejecting, and modifying suggestions
- Develop efficient workflows using Copilot in RStudio

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction

GitHub Copilot functions as an advanced autocompletion tool in RStudio, 
going beyond simple syntax completion to suggest entire lines or blocks of code. 
This chapter covers how to use Copilot effectively as an autocompletion assistant.

## How Copilot Works

GitHub Copilot uses machine learning models trained on billions of lines of public code to:

- Analyze the context of your current code
- Understand comments and function names
- Predict what you're trying to accomplish
- Generate relevant code suggestions

::::::::::::::::::::::::::::::::::::: callout

### Context is Key

Copilot examines:

- Your current file's code
  - Comments you've written
  - Variable and function names
  - The structure of your code
- Open files in RStudio (depending on your settings)

The more context you provide, the better the suggestions!

::::::::::::::::::::::::::::::::::::::::::::::::

## Writing Effective Comments for Better Suggestions

### Comment-Driven Development

One of the most effective ways to use Copilot is to write descriptive comments first:

**Good Example:**

```r
# Load data from CSV, remove rows with missing values, and convert date column to Date type
```

**Less Effective:**

```r
# Load data
```

::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 1: Practice Writing Effective Comments

Write a detailed comment describing what you want the code to do for the following scenario:

You need to create a function that takes a data frame of student grades, 
calculates the average grade for each student, and returns only students with an average above 70.

:::::::::::::::::::::::: solution 

## Example Solution

```r
# Function to calculate average grades per student and filter for high performers
# Input: data frame with columns 'student_name' and 'grade'
# Output: data frame with columns 'student_name' and 'avg_grade' for students with avg > 70
```

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

## Accepting and Managing Suggestions

### Keyboard Shortcuts

- **Tab:** Accept the entire suggestion
- **Esc:** Dismiss the current suggestion
- **Ctrl + Shift + L** or **Cmd + Shift + L:** Request a new suggestion

### Partial Acceptance

You can accept suggestions word-by-word:

- **Ctrl + →** or **Cmd + →:** Accept next word
- This allows you to use parts of a suggestion while continuing to type

::::::::::::::::::::::::::::::::::::: callout

### Ghost Text

Copilot suggestions appear as gray "ghost text" in your editor. 
This makes it easy to see suggestions without disrupting your coding flow.

::::::::::::::::::::::::::::::::::::::::::::::::

## Techniques for Getting Better Suggestions

### 1. Provide Clear Function Signatures

Start with a clear function definition:

```r
# Copilot works better when you define function structure first
calculate_summary_stats <- function(data, group_var) {
  # Calculate mean, median, and sd for each group
  
}
```

### 2. Use Meaningful Variable Names

```r
# Better - descriptive names help Copilot understand context
student_grades_df <- read.csv("grades.csv")

# Less helpful
df <- read.csv("grades.csv")
```

### 3. Break Down Complex Tasks

Instead of asking for everything at once:

```r
# Step 1: Load and clean data
# Load CSV file with student information

# Step 2: Calculate metrics
# Calculate average grade per student

# Step 3: Filter results
# Keep only students with average above threshold
```

::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 2: Experiment with Context

Try generating code for the same task with different levels of context:

1. Just type: `read.csv(`
2. Add a comment first: `# Load student data from grades.csv` then `read.csv(`
3. Add more context: 

 ```r
 # Data has columns: student_id, name, grade, date
 # Load student data from grades.csv with explicit column types
 ```
 then `read.csv(`

:::::::::::::::::::::::: solution 

## Observation

You should notice that:

- With minimal context, Copilot might just complete the parentheses
- With a comment, it might suggest the filename
- With detailed context, it might suggest the filename AND additional parameters like `stringsAsFactors = FALSE` or `header = TRUE`

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

## Working with Different Types of Suggestions

### Single-Line Completions

Best for:

- Completing function calls
- Finishing variable assignments
- Adding package imports

Example:

```r
library(# Copilot suggests: tidyverse)
```

### Multi-Line Suggestions

Best for:

- Function implementations
- Code blocks (if/else, loops)
- Multiple related operations

Example:

```r
# Function to plot distribution with ggplot2
plot_distribution <- function(data, column) {
  # Copilot may suggest entire function body
}
```

## Best Practices for Efficient Workflow

### 1. Review Before Accepting

Always read the suggestion before pressing `Tab` key:

- Check for logical errors
- Verify it matches your intent
- Look for security issues

### 2. Iterate and Refine

- Accept a suggestion as a starting point
- Modify it to fit your specific needs
- Add error handling and edge cases

### 3. Combine with Traditional Coding

- Use Copilot for repetitive tasks
- Code critical logic yourself
- Let Copilot help with boilerplate

::::::::::::::::::::::::::::::::::::: callout

### Maintain Your Coding Skills

While Copilot is helpful, continue to:

- Understand the code you're using
- Practice writing code without assistance
- Learn from the suggestions Copilot provides

::::::::::::::::::::::::::::::::::::::::::::::::

## Common Patterns and Use Cases

### Data Manipulation with dplyr

```r
# Copilot excels at suggesting dplyr pipelines
# Filter data for specific conditions and group by category
data %>%
  # Copilot suggests the rest
```

### Creating Plots with ggplot2

```r
# Create a scatter plot with regression line
ggplot(data, aes(x = height, y = weight)) +
  # Copilot suggests layers
```

### Writing Functions

```r
# Function to validate email addresses
validate_email <- function(email) {
  # Copilot suggests regex patterns and validation logic
}
```

::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 3: Build a Function with Copilot

Use Copilot to help you create a function that:

1. Takes a numeric vector as input
2. Removes outliers (values > 3 standard deviations from mean)
3. Returns the cleaned vector

Start with a descriptive comment and function signature.

:::::::::::::::::::::::: solution 

## Example Approach

```r
# Function to remove outliers from a numeric vector
# Outliers are defined as values more than 3 SD from the mean
# Input: numeric vector
# Output: numeric vector with outliers removed
remove_outliers <- function(x, sd_threshold = 3) {
  # Let Copilot suggest the implementation
  # It might suggest something like:
  mean_x <- mean(x, na.rm = TRUE)
  sd_x <- sd(x, na.rm = TRUE)
  x[abs(x - mean_x) <= sd_threshold * sd_x]
}
```

Remember to test the function with sample data!

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

## Troubleshooting Suggestions

### Copilot Suggests Incorrect Code

- Provide more specific comments
- Add type hints or example data structures
- Break down the task into smaller steps

### No Suggestions Appear

- Check that Copilot is enabled
- Verify your internet connection
- Provide more context with comments
- Wait a moment - suggestions can take a second to generate

### Suggestions Don't Match Your Intent

- Rewrite your comment more specifically
- Add examples of input/output
- Specify the packages you want to use

## Advanced Tips

### Specifying Packages

```r
# Using dplyr and tidyr to reshape data
```

### Requesting Specific Approaches

```r
# Using base R (not tidyverse) to calculate mean by group
```

### Setting Constraints

```r
# Function must handle NA values and return informative error messages
```

::::::::::::::::::::::::::::::::::::: keypoints 

- Copilot generates suggestions based on context from your code and comments
- Write clear, descriptive comments to get better suggestions
- Use Tab to accept, and Esc to dismiss suggestions
- Break complex tasks into smaller steps for more accurate suggestions
- Always review and test AI-generated code before using it
- Combine Copilot assistance with your own coding expertise for best results

::::::::::::::::::::::::::::::::::::::::::::::::
