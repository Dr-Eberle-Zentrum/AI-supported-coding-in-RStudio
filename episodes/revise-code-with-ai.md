---
title: "Revise Your Code with AI"
teaching: 25
exercises: 15
---

:::::::::::::::::::::::::::::::::::::: questions 

- How can I use AI to check and improve my code?
- What are effective strategies for code review with AI assistants?
- How do I use chat interfaces for iterative code refinement?
- When should I trust AI suggestions for code revisions?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Use AI chat interfaces to review and analyze code
- Identify code issues with AI assistance
- Iteratively refine code based on AI feedback
- Validate AI suggestions critically
- Develop a workflow for AI-assisted code revision

::::::::::::::::::::::::::::::::::::::::::::::::

## Using AI directively

![Directive AI usage](ai-mode-2.png)


AI-powered tools can serve as an additional pair of eyes when reviewing and improving your code. 
This chapter explores how to effectively use AI chat interfaces to check, revise, and validate your R code, ensuring better quality and maintainability.

## Why Use AI for Code Review?

AI assistants can help identify:

- **Logic errors**: Potential bugs or incorrect implementations
- **Performance issues**: Inefficient code patterns
- **Style problems**: Code that doesn't follow best practices
- **Documentation gaps**: Missing or unclear comments
- **Security vulnerabilities**: Potential security risks

::::::::::::::::::::::::::::::::::::: callout

### AI as a Complement, Not Replacement

AI code review should complement, not replace:

- Your own understanding of the code
- Human peer reviews
- Automated testing and linting tools
- Domain expertise

::::::::::::::::::::::::::::::::::::::::::::::::

## Setting Up for AI Code Review

### Using GitHub Copilot Chat in your browser

Currently (as of end 2025), RStudio has no built-in AI chat interface

However, you can use GitHub Copilot Chat within your browser.

To this end:

- Navigate to [https::github.com/copilot]
- For an extended list of models:
  - Ensure you have a GitHub Copilot subscription
  - Sign in

If you have any other AI chat interface you prefer (e.g., ChatGPT, Claude), 
you can use that as well.

When using a browser, you have to manually copy and paste code snippets between 
RStudio and the chat interface to get reviews and suggestions.
While this is less seamless than an integrated solution, 
it still allows you to leverage AI for code review.

### Alternative: Use the `chattr` app within RStudio

The [`chattr` package](https://mlverse.github.io/chattr/) provides an interface 
to chat with AI models directly within RStudio.

The `chattr_app()` function will open a Shiny app where you can interact with various AI models.
Alternatively, you can run the app via the RStudio "Addins"" menu by selecting "Open chat".

Unfortunately, running the chat interface will "block" your R session until you close the app.

A workaround is to run the app in "job" mode using

```r
chattr::chattr_app(as_job = TRUE)
```

That way, you can continue working in your main R session while chatting with the AI in a separate window.
The con is that the chattr app won't be able to directly interact with your current document in RStudio.


Via the same "Addins" menu, you can also **select code in your R script and choose "Send prompt"** to get AI feedback 
on that specific code snippet, which will be copied back directly below your selection.

As of now, I personally find using GitHub Copilot Chat in the browser more flexible for code review tasks,
but the `chattr` package is a promising option for integrated RStudio workflows.

If you are interested in a more sophisticated AI integration into your IDE,
you might have to consider to try another IDE such as 
[Positron](https://positron.posit.co/) or 
[Visual Studio Code](https://code.visualstudio.com/).


## Basic Code Review Workflow

The following steps are a general workflow for using AI to review and improve your R code.

### Step 1: Request an Initial Review

Select your code and ask AI to review it:

```r
# Example code to review
calculate_mean <- function(numbers) {
  sum(numbers) / length(numbers)
}
```

**Prompt for AI:**
> Review this function for potential issues and suggest improvements.

::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 1: Basic Code Review

Ask AI to review the following function. What issues does it identify?

```r
process_data <- function(data) {
  result <- data[data$value > 0]
  mean_val <- sum(result$value) / nrow(result)
  return(mean_val)
}
```

:::::::::::::::::::::::: solution 

## Issues AI Might Identify

1. **No NA handling**: Function will fail if there are NA values
2. **Division by zero**: If no rows match the condition, `nrow(result)` is 0
3. **Column existence**: Assumes `value` column exists without checking
4. **No input validation**: Doesn't verify `data` is a data frame

**Improved version:**
```r
process_data <- function(data) {
  # Input validation
  if (!is.data.frame(data)) {
    stop("Input must be a data frame")
  }
  if (!"value" %in% names(data)) {
    stop("Data frame must contain 'value' column")
  }
  
  # Filter and calculate
  result <- data[data$value > 0 & !is.na(data$value), ]
  
  if (nrow(result) == 0) {
    warning("No positive values found")
    return(NA)
  }
  
  mean(result$value, na.rm = TRUE)
}
```

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

### Step 2: Ask Specific Questions

Be specific about what you want to check:

**Good prompts:**

- "Does this function handle edge cases correctly?"
- "Are there any performance bottlenecks in this loop?"
- "Is this code following tidyverse style guidelines?"
- "Could this code be more readable?"

**Less effective prompts:**

- "Is this good?"
- "Check this code"

### Step 3: Request Improvements

```r
# Original code
for(i in 1:length(data)) {
  result[i] <- data[i] * 2
}
```

**Prompt:**
> How can I make this code more efficient and R-idiomatic?

**AI might suggest:**

```r
# Vectorized approach (much faster)
result <- data * 2
```

## Iterative Refinement Process

### Round 1: Initial Review

```r
# Your initial code
analyze_sales <- function(sales_data) {
  total <- 0
  for(i in 1:nrow(sales_data)) {
    total <- total + sales_data[i, "amount"]
  }
  return(total / nrow(sales_data))
}
```

**AI Feedback:** "This uses a slow loop. Consider vectorization."

### Round 2: Apply Suggestions

```r
analyze_sales <- function(sales_data) {
  mean(sales_data$amount)
}
```

**AI Feedback:** "Good! Consider adding NA handling and input validation."

### Round 3: Further Refinement

```r
analyze_sales <- function(sales_data) {
  if (!is.data.frame(sales_data)) {
    stop("Input must be a data frame")
  }
  if (!"amount" %in% names(sales_data)) {
    stop("Data must contain 'amount' column")
  }
  
  mean(sales_data$amount, na.rm = TRUE)
}
```

::::::::::::::::::::::::::::::::::::: callout

### Iterative Improvement

Don't expect perfect code in one iteration. Use AI as a collaborative partner:

1. Get initial feedback
2. Make changes
3. Ask for review again
4. Repeat until satisfied

::::::::::::::::::::::::::::::::::::::::::::::::

## Common Code Issues AI Can Help Identify

### 1. Logic Errors

```r
# Problematic code
if (x > 0 & y > 0) {  # What if x or y is NA?
  process(x, y)
}
```

**AI can suggest:**

```r
if (!is.na(x) && !is.na(y) && x > 0 && y > 0) {
  process(x, y)
}
```

Did you notice the change from `&` to `&&`? If you don't know why, ask AI! 

### 2. Performance Problems

```r
# Slow: Growing vector in loop
result <- c()
for(i in 1:10000) {
  result <- c(result, calculate(i))
}
```

**AI can suggest:**

```r
# Fast: Pre-allocate vector
result <- vector("numeric", 10000)
for(i in 1:10000) {
  result[i] <- calculate(i)
}

# Even better: Vectorize if possible using sapply() or purrr
result <- purrr::map_dbl(1:10000, calculate)
```

### 3. Code Readability

```r
# Hard to read
f <- function(x, y, z) { x + y * z / (x - y) }
```

**AI can suggest:**

```r
# More readable
calculate_metric <- 
  function(base_value, multiplier, divisor) {
    adjustment <- multiplier * divisor
    denominator <- base_value - multiplier
    
    base_value + (adjustment / denominator)
  }
```

::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 2: Iterative Code Improvement

Start with this code and iteratively improve it with AI assistance:

```r
my_function <- function(x) {
  y <- c()
  for(i in 1:length(x)) {
    if(x[i] > 0) {
      y <- c(y, x[i] * 2)
    }
  }
  return(y)
}
```

Ask AI to help you:

1. Improve performance
2. Add error handling
3. Improve readability
4. Add documentation

:::::::::::::::::::::::: solution 

## Improved Version After Iterations

```r
#' Double positive values in a numeric vector
#'
#' Takes a numeric vector and returns a new vector containing
#' only the positive values, each doubled.
#'
#' @param x A numeric vector
#' @return A numeric vector of doubled positive values
#' @examples
#' double_positives(c(-1, 2, -3, 4))  # Returns c(4, 8)
double_positives <- function(x) {
  # Input validation
  if (!is.numeric(x)) {
    stop("Input must be a numeric vector")
  }
  
  # Vectorized filtering and transformation
  positive_values <- x[x > 0 & !is.na(x)]
  positive_values * 2
}
```

Key improvements:

- Descriptive function name
- Roxygen documentation
- Input validation
- Vectorized operations (much faster)
- `NA` handling

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

## Using Chat for Code Explanation

AI can help you understand unfamiliar code:

```r
# Complex code you found
result <- df %>%
  group_by(category) %>%
  summarise(
    mean_val = mean(value, na.rm = TRUE),
    .groups = "drop"
  ) %>%
  filter(mean_val > quantile(mean_val, 0.75))
```

**Prompt:**

> Explain what this code does step by step.

**AI response would explain:**

1. Groups data by category
2. Calculates mean value per category
3. Drops grouping structure
4. Filters for top 25% of means

Often it is a good idea to ask the AI to **incorporate explanations as comments in the code itself**.
That way, you have both the code and the explanation together for future reference and rereading.

## Double-Checking AI Suggestions

### Always Validate AI Recommendations

```r
# AI suggests: "Use this for better performance"
result <- parallel::mclapply(data, complex_function)
```

**Questions to ask yourself:**

1. Does this actually work with my data?
2. Is parallel processing appropriate here?
3. Will this work on all platforms (Windows issues with mclapply)?
4. Is the complexity worth the performance gain?

::::::::::::::::::::::::::::::::::::: callout

### Test AI Suggestions

Never blindly accept AI code suggestions:

- Run the code with test data
- Verify results match expectations
- Check edge cases
- Benchmark performance claims
- Ensure compatibility with your environment

::::::::::::::::::::::::::::::::::::::::::::::::

### Creating Test Cases

Use AI to help generate tests:

**Prompt:**

> Generate test cases for this function, including edge cases.

```r
# Your function
safe_divide <- function(a, b) {
  if (b == 0) return(NA)
  a / b
}
```

**AI-generated tests:**

```r
# Test cases
test_that("safe_divide works correctly", {
  expect_equal(safe_divide(10, 2), 5)
  expect_equal(safe_divide(0, 5), 0)
  expect_true(is.na(safe_divide(5, 0)))
  expect_true(is.na(safe_divide(Inf, 0)))
  expect_equal(safe_divide(-10, 2), -5)
})
```

While this will provide the needed code for tests, 
make sure to **review the tested values** and adapt the tests to your specific needs.

## Advanced Code Review Techniques

### 1. Security Review

**Prompt:**

> Review this code for security vulnerabilities.

```r
# Potentially unsafe
query <- paste0("SELECT * FROM users WHERE id = ", user_input)
```

**AI might warn:** SQL injection risk!

### 2. Style Consistency

**Prompt:**

> Does this code follow tidyverse style guidelines?

```r
# Inconsistent style
myFunction<-function(x,y){return(x+y)}
```

**AI suggests:**

```r
# Consistent style
my_function <- function(x, y) {
  x + y
}
```

### 3. Documentation Review

**Prompt:**

> Is this function well-documented? Suggest improvements.

```r
calc <- function(x, y) {
  x * y + mean(x)
}
```

**AI suggests adding:**

```r
#' Calculate weighted metric
#'
#' Multiplies two vectors element-wise and adds the mean of the first vector
#'
#' @param x Numeric vector for values
#' @param y Numeric vector for weights
#' @return Numeric vector of weighted values plus mean adjustment
calc <- function(x, y) {
  x * y + mean(x)
}
```

::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 3: Comprehensive Code Review

Perform a complete AI-assisted review of this analysis function:

```r
analyze <- function(d) {
  d2 <- d[d$val > 0]
  m <- sum(d2$val) / length(d2$val)
  s <- sqrt(sum((d2$val - m)^2) / length(d2$val))
  list(m, s)
}
```

Review for:

1. Correctness
2. Efficiency
3. Readability
4. Documentation
5. Error handling

:::::::::::::::::::::::: solution 

## Comprehensive Improved Version

```r
#' Calculate mean and standard deviation for positive values
#'
#' Filters a data frame to positive values in the specified column
#' and calculates descriptive statistics
#'
#' @param data A data frame containing the data to analyze
#' @param value_col Name of the column containing values (default: "val")
#' @return A named list with 'mean' and 'sd' of positive values
#' @examples
#' analyze_positive_values(data.frame(val = c(-1, 2, 3, 4)))
analyze_positive_values <- function(data, value_col = "val") {
  # Input validation
  if (!is.data.frame(data)) {
    stop("Input must be a data frame")
  }
  if (!value_col %in% names(data)) {
    stop(paste("Column", value_col, "not found in data"))
  }
  if (!is.numeric(data[[value_col]])) {
    stop(paste("Column", value_col, "must be numeric"))
  }
  
  # Filter positive values and remove NAs
  positive_values <- data[[value_col]][
    data[[value_col]] > 0 & !is.na(data[[value_col]])
  ]
  
  # Check if any values remain
  if (length(positive_values) == 0) {
    warning("No positive values found")
    return(list(mean = NA, sd = NA))
  }
  
  # Calculate statistics using built-in functions
  # (more accurate than manual calculation)
  list(
    mean = mean(positive_values),
    sd = sd(positive_values)
  )
}
```

Improvements:

- Clear, descriptive name
- Full documentation
- Input validation
- Column name parameter
- `NA` handling
- Edge case handling
- Uses built-in statistical functions
- Named list output

What you might have noticed at this point: well documented and robust code often 
spends more lines on validation and documentation than on the actual logic itself.

**That's fine!!!**

Writing maintainable code is more important than keeping it short.

From this code, you can also automatically generate documentation pages using `roxygen2`,
 which is a great bonus for future users (including yourself).
Or you can use the documentation to generate vignettes or tutorials.

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

## Best Practices for AI-Assisted Code Review

### 1. Start with Specific Questions

*Instead of*: "Review this code"

**Try**: "Does this function handle missing data correctly?"

### 2. Review in Small Chunks

- Don't send entire scripts for review
- Focus on one function or logical block at a time
- Easier to understand and act on feedback

### 3. Ask "Why" Questions

- "Why is this approach better?"
- "Why might this fail?"
- "Why is this more efficient?"

Understanding helps you learn, not just copy.

### 4. Combine Multiple Perspectives

- AI review
- Peer review
- Automated linting (e.g. [`lintr` package](https://lintr.r-lib.org/))
- Testing (e.g. [`testthat` package](https://testthat.r-lib.org/))

### 5. Document Changes

Keep track of improvements.

```r
# Version 1 (original): Simple but no error handling
# Version 2 (after AI review): Added input validation
# Version 3 (after testing): Improved edge case handling
```

But best not via comments, rather via a proper version control system such as Git.
The latter is especially important when collaborating in teams and neatly integrated into RStudio.

In combination with GitHub, you can even use AI tools to help you write better commit messages,
set up automated post-push actions for linting, testing, and documentation generation.
And the GitHub Copilot can even help you via the GitHub web interface to review pull requests, 
suggest solutions for issues and improvements, as we will discuss in more detail in later chapters.


::::::::::::::::::::::::::::::::::::: discussion

### Group Discussion

Discuss with your peers:

- What types of code issues have you discovered using AI review?
- Have you encountered situations where AI gave incorrect advice?
- How do you balance AI suggestions with your own judgment?
- What are the limitations of AI code review compared to human review?

:::::::::::::::::::::::::::::::::::::::::::::::::::

## Limitations and Cautions

### AI Cannot Replace

- **Domain expertise**: Understanding of your specific field
- **Context awareness**: Knowledge of project history and constraints
- **Testing**: Actual execution and validation
- **Team standards**: Specific conventions in your organization

### Common AI Mistakes

- Suggesting overly complex solutions
- Not understanding project-specific constraints
- Proposing outdated or deprecated approaches
- Missing subtle domain-specific issues

### When to Seek Human Review

- Security-critical code
- Complex algorithms
- Code with business logic
- Performance-critical sections
- Code you don't fully understand

::::::::::::::::::::::::::::::::::::: keypoints 

- AI chat interfaces provide valuable code review assistance
- Use iterative refinement: review, improve, and re-review
- Ask specific questions about correctness, performance, and style
- Always validate and test AI suggestions before accepting them
- Combine AI review with human peer review and automated tools
- Be aware of AI limitations and seek human expertise for critical code
- Document the review process and improvements made

::::::::::::::::::::::::::::::::::::::::::::::::
