---
title: "Risks, Drawbacks and Responsibilities with AI Usage"
teaching: 30
exercises: 15
---

:::::::::::::::::::::::::::::::::::::: questions 

- What can go wrong when using AI coding assistants?
- What are my responsibilities as a developer when using AI?
- When is AI usage inappropriate or a no-go?
- What are the side effects of heavy AI reliance?
- Why do LLMs produce incorrect code and how can I avoid it?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Understand potential risks and pitfalls of AI-assisted coding
- Recognize your responsibilities as a developer using AI tools
- Identify scenarios where AI usage is inappropriate
- Learn strategies to mitigate risks and verify AI-generated code
- Develop awareness of long-term effects of AI dependence
- Apply best practices for responsible AI usage in coding

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction

While AI coding assistants like GitHub Copilot can significantly enhance productivity, they come with important risks, drawbacks, and responsibilities. Understanding these challenges is crucial for using AI tools effectively and ethically. This lesson explores what can go wrong, your responsibilities as a user, and how to navigate the complex landscape of AI-assisted development.

::::::::::::::::::::::::::::::::::::: callout

### The Double-Edged Sword

AI coding assistants are powerful tools that can accelerate development, but they require careful use. Just as you wouldn't use a power tool without understanding safety precautions, you shouldn't use AI coding assistants without understanding their limitations and risks.

::::::::::::::::::::::::::::::::::::::::::::::::

## What Can Go Wrong?

### 1. Incorrect or Buggy Code

AI models can generate code that appears correct but contains subtle bugs:

**Example: Off-by-One Errors**
```r
# AI might suggest
filter_data <- function(data, threshold) {
  data[1:length(data) - 1]  # Bug: loses last element
}

# Correct version
filter_data <- function(data, threshold) {
  data[data > threshold]
}
```

**Why this happens:**
- AI learns from patterns in training data, including buggy code
- AI doesn't execute or test the code it generates
- Subtle logic errors are harder for pattern-matching to detect

### 2. Security Vulnerabilities

AI may suggest code with security flaws:

```r
# INSECURE: AI might suggest
execute_query <- function(user_input) {
  query <- paste0("SELECT * FROM users WHERE name = '", user_input, "'")
  dbGetQuery(conn, query)  # SQL injection vulnerability!
}

# SECURE: Use parameterized queries
execute_query <- function(user_input) {
  query <- "SELECT * FROM users WHERE name = ?"
  dbGetQuery(conn, query, params = list(user_input))
}
```

**Security risks include:**
- SQL injection vulnerabilities
- Cross-site scripting (XSS) in web applications
- Hardcoded credentials or API keys
- Unsafe file operations
- Improper input validation

### 3. Inefficient or Non-Performant Code

AI may suggest code that works but performs poorly:

```r
# INEFFICIENT: AI might suggest
calculate_means <- function(data) {
  results <- list()
  for(i in 1:ncol(data)) {
    results[[i]] <- mean(data[, i])
  }
  return(unlist(results))
}

# EFFICIENT: Vectorized approach
calculate_means <- function(data) {
  colMeans(data)
}
```

### 4. License and Copyright Issues

AI models are trained on public code repositories, which may include:
- Code with restrictive licenses (GPL, AGPL)
- Proprietary code that shouldn't have been public
- Code with unclear licensing

**Risks:**
- Inadvertently incorporating GPL code into proprietary projects
- Copyright infringement claims
- License compliance violations

::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 1: Identify the Bug

Ask an AI assistant to generate a function that removes duplicates from a vector while preserving order. Test the result with edge cases:

```r
test_data <- c(1, 2, 2, 3, 1, 4, NA, 5, NA)
```

What might go wrong?

:::::::::::::::::::::::: solution 

## Potential Issues

AI might generate code that:
1. **Doesn't handle NA values correctly:**
   ```r
   # Might remove all NAs or fail
   unique(test_data)  # This actually works, but AI might suggest worse
   ```

2. **Uses inefficient approaches:**
   ```r
   # Slow for large vectors
   result <- c()
   for(x in test_data) {
     if(!(x %in% result)) result <- c(result, x)
   }
   ```

3. **Doesn't preserve order as required:**
   ```r
   # sort() changes order
   sort(unique(test_data))
   ```

**Better solution:**
```r
remove_duplicates <- function(x) {
  x[!duplicated(x)]  # Preserves order, handles NA
}
```

**Lesson:** Always test AI-generated code with edge cases!

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

## Your Responsibilities as an AI User

### 1. Code Ownership and Accountability

**You are ultimately responsible for all code in your project**, regardless of whether it was written by you or suggested by AI.

**This means:**
- You must understand every line of code you commit
- You are accountable for bugs, security issues, and performance problems
- You cannot blame the AI if something goes wrong
- You must be able to explain and defend your code choices

### 2. Verification and Testing

**Never blindly accept AI suggestions.** Always:

```r
# Example verification workflow
ai_suggested_function <- function(data) {
  # [AI-generated code here]
}

# REQUIRED: Create comprehensive tests
test_that("ai_suggested_function works correctly", {
  # Test normal cases
  expect_equal(ai_suggested_function(c(1, 2, 3)), expected_result)
  
  # Test edge cases
  expect_error(ai_suggested_function(NULL))
  expect_equal(ai_suggested_function(c()), expected_empty_result)
  expect_equal(ai_suggested_function(c(NA, 1, 2)), expected_with_na)
  
  # Test performance for large inputs
  large_data <- rep(1:1000, 1000)
  expect_lt(system.time(ai_suggested_function(large_data))[3], 1.0)
})
```

### 3. Security Awareness

You must:
- Review all AI-generated code for security vulnerabilities
- Never include sensitive data in prompts to AI tools
- Understand that code sent to cloud-based AI may be logged
- Follow security best practices even when AI suggests otherwise

::::::::::::::::::::::::::::::::::::: callout

### Data Privacy Alert

When using cloud-based AI assistants:
- Your code snippets may be sent to external servers
- Avoid including passwords, API keys, or sensitive data
- Check your organization's policies on AI tool usage
- Consider using local AI models for sensitive projects

::::::::::::::::::::::::::::::::::::::::::::::::

### 4. Continuous Learning

**Don't let AI replace your learning:**
- Use AI as a learning tool, not a crutch
- Understand why suggested solutions work
- Research functions and techniques you don't recognize
- Build your own expertise alongside AI assistance

### 5. Attribution and Transparency

Be transparent about AI usage:
- Document when AI significantly contributed to code
- Follow your organization's policies on AI disclosure
- Consider adding comments noting AI-assisted sections
- Be honest in academic and professional contexts

## When AI Usage Is a No-Go

### 1. Critical Systems

**Avoid AI for:**
- Medical device software
- Financial transaction systems
- Safety-critical aerospace or automotive code
- Security authentication systems
- Life-dependent systems

**Why:** The stakes are too high for AI-generated code without extensive human review and testing.

### 2. Specialized or Novel Algorithms

**Be cautious with:**
- Cutting-edge research implementations
- Domain-specific algorithms not well-represented online
- Novel statistical methods
- Proprietary business logic

**Why:** AI training data may not include correct implementations of specialized techniques.

### 3. Highly Regulated Domains

**Extra caution in:**
- Healthcare (HIPAA compliance)
- Finance (SOX, PCI-DSS compliance)
- Government (security clearances required)
- Privacy-sensitive applications (GDPR)

**Why:** Compliance requirements demand human oversight and documentation that AI cannot provide.

### 4. Learning Fundamentals

**Don't use AI when:**
- Learning a new programming language
- Studying fundamental algorithms and data structures
- Completing academic assignments (unless explicitly allowed)
- Building foundational skills

**Why:** You need to develop core competencies yourself.

::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 2: Ethical Scenarios

Discuss these scenarios with a partner:

1. You're a student. Your professor hasn't explicitly forbidden AI use. Is it okay to use Copilot for homework?

2. You're on a tight deadline. AI generates a function you don't fully understand, but it seems to work. Do you use it?

3. You discover that AI-suggested code solves your problem but uses a GPL license library in a proprietary project. What do you do?

:::::::::::::::::::::::: solution 

## Discussion Points

**Scenario 1 - Academic Integrity:**
- If not explicitly allowed, assume it's not permitted
- Academic assignments are for learning, not just completion
- Using AI without understanding violates learning objectives
- **Best practice:** Ask your professor about AI policy

**Scenario 2 - Code Understanding:**
- Using code you don't understand is dangerous
- It may have bugs or security issues you can't detect
- You won't be able to maintain or debug it later
- **Best practice:** Take time to understand, refactor if needed, or find another solution

**Scenario 3 - License Compliance:**
- Using GPL code in proprietary software violates the license
- This could lead to legal issues for your organization
- **Best practice:** Remove the code and find an alternative with a compatible license (MIT, Apache, BSD)

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

## Side Effects of Heavy AI Reliance

### 1. Skill Atrophy

**Long-term risks:**
- Reduced ability to write code from scratch
- Weakened problem-solving skills
- Decreased understanding of fundamentals
- Dependency on AI availability

**Example:**
A developer who always uses AI for basic tasks may struggle when:
- Working offline
- Debugging complex issues
- Interviewing for new positions
- Mentoring junior developers

### 2. Reduced Code Understanding

**Consequences:**
- Difficulty maintaining code you didn't write or understand
- Inability to debug when issues arise
- Challenges explaining code to colleagues
- Problems adapting code to changing requirements

### 3. Homogenization of Code

**Problems:**
- Everyone's code starts looking similar (AI patterns)
- Loss of creative problem-solving approaches
- Reduced innovation in software design
- "Cargo cult" programming (copying without understanding)

### 4. False Confidence

**Dangers:**
- Overestimating code quality because it "looks professional"
- Underestimating testing needs
- Reduced code review rigor
- Faster development at the cost of quality

::::::::::::::::::::::::::::::::::::: callout

### Maintaining Skills While Using AI

**Balance is key:**
- Set aside time for coding without AI assistance
- Practice fundamental skills regularly
- Do code katas or programming challenges manually
- Review and understand all AI-generated code
- Explain solutions to others to test your understanding

::::::::::::::::::::::::::::::::::::::::::::::::

## Why LLMs Produce Wrong Code

### 1. Pattern Matching, Not Understanding

**LLMs don't "understand" code:**
- They predict likely token sequences based on training data
- They don't execute code mentally to verify correctness
- They don't reason about edge cases
- They replicate patterns even when inappropriate

**Example:**
```r
# AI might suggest this pattern because it's common
calculate_average <- function(x) {
  sum(x) / length(x)  # Fails with NAs!
}

# But context might require
calculate_average <- function(x) {
  mean(x, na.rm = TRUE)  # Handles NAs correctly
}
```

### 2. Training Data Limitations

**Issues with training data:**
- Contains buggy code from public repositories
- May be outdated (not current best practices)
- Overrepresents certain languages and frameworks
- May include deprecated or insecure patterns

### 3. Context Window Limitations

**LLMs have limited context:**
- Can't see entire project structure
- Miss important constraints from other files
- Don't know your specific requirements
- Lack domain-specific knowledge

### 4. No Execution or Testing

**Critical limitation:**
- AI generates code but doesn't run it
- No feedback loop from actual execution
- Can't verify correctness through testing
- Doesn't catch runtime errors

::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 3: Prompt Engineering for Better Code

Try improving AI-generated code quality by refining your prompts. Compare results:

**Poor prompt:**
> Write a function to process data

**Better prompt:**
> Write an R function that filters a data frame to include only rows where the 'value' column is positive and non-NA. Include input validation, error handling, and roxygen2 documentation.

Try both prompts with your AI assistant. How do the results differ?

:::::::::::::::::::::::: solution 

## Observations

**Poor prompt typically produces:**
- Generic, vague code
- No error handling
- No documentation
- Assumes undocumented column names
- Doesn't handle edge cases

**Better prompt typically produces:**
- More specific, targeted code
- Input validation
- Documentation
- Explicit handling of requirements
- Better edge case coverage

**Key lessons:**
1. Specific prompts → better results
2. State requirements explicitly
3. Request error handling and documentation
4. Mention edge cases you care about
5. Specify coding standards or style

**But remember:** Even with great prompts, always verify the output!

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

## How to Avoid AI-Generated Errors

### 1. Adopt a Verification Mindset

**Question everything:**
```r
# When AI suggests code, ask yourself:
# - Do I understand what this does?
# - What are the assumptions?
# - What could go wrong?
# - Are there edge cases?
# - Is this efficient?
# - Is this secure?
```

### 2. Use Comprehensive Testing

```r
# Create tests BEFORE accepting AI code
test_that("function handles all cases", {
  # Normal cases
  expect_equal(my_function(normal_input), expected_output)
  
  # Edge cases
  expect_equal(my_function(c()), expected_empty)
  expect_equal(my_function(NULL), expected_null)
  expect_true(is.na(my_function(c(NA))))
  
  # Error cases
  expect_error(my_function("wrong type"))
  expect_error(my_function(-1))
  
  # Boundary cases
  expect_equal(my_function(c(0)), expected_zero)
  expect_equal(my_function(c(Inf)), expected_inf)
})
```

### 3. Code Review Process

**Always review AI-generated code for:**
- Correctness of logic
- Error handling
- Input validation
- Performance implications
- Security vulnerabilities
- Code style and readability
- Documentation quality

### 4. Iterative Refinement

Don't accept the first suggestion:
```r
# Round 1: AI suggests basic solution
# Round 2: Request error handling
# Round 3: Request performance optimization
# Round 4: Request documentation
# Final: Human review and testing
```

### 5. Use Linting and Static Analysis

```r
# Use automated tools alongside AI
library(lintr)
lint("my_script.R")

# Check code style
library(styler)
style_file("my_script.R")

# Static analysis
# Run R CMD check on packages
```

### 6. Benchmark and Profile

```r
# Verify performance claims
library(microbenchmark)

microbenchmark(
  ai_version = ai_suggested_function(data),
  manual_version = my_implementation(data),
  times = 100
)

# Profile to find bottlenecks
library(profvis)
profvis({
  result <- ai_suggested_function(large_data)
})
```

## Best Practices for Responsible AI Usage

### 1. The 80/20 Rule

Use AI for the 80% of straightforward, repetitive tasks. Reserve human expertise for the critical 20% involving:
- Complex algorithms
- Security-sensitive code
- Performance optimization
- Architectural decisions
- Domain-specific logic

### 2. Treat AI as a Junior Developer

Think of AI as a smart but inexperienced assistant:
- It needs clear instructions
- It requires supervision
- Its work must be reviewed
- It shouldn't handle critical tasks alone
- It can help with routine work

### 3. Document AI Usage

```r
# Consider adding comments for transparency
#' Calculate weighted average
#'
#' This function was initially drafted with AI assistance
#' and subsequently reviewed, tested, and validated.
#'
#' @param values Numeric vector of values
#' @param weights Numeric vector of weights
#' @return Weighted average
calculate_weighted_avg <- function(values, weights) {
  # Implementation here
}
```

### 4. Continuous Skill Development

**Maintain your skills:**
- Practice coding without AI regularly
- Study algorithms and data structures
- Read high-quality code from experts
- Contribute to code reviews
- Teach others what you learn

### 5. Stay Informed

AI capabilities and limitations change rapidly:
- Follow updates to tools you use
- Learn about new AI capabilities
- Understand evolving best practices
- Participate in communities discussing AI use

::::::::::::::::::::::::::::::::::::: discussion

### Group Discussion

Discuss with your peers:

1. Have you encountered situations where AI-generated code was wrong? What happened?

2. How do you balance productivity gains from AI with the need to maintain your coding skills?

3. What policies should organizations have regarding AI coding assistant use?

4. How might AI tools change the role of programmers in the future?

5. What ethical considerations should guide AI use in software development?

:::::::::::::::::::::::::::::::::::::::::::::::::::

## Legal and Ethical Considerations

### Copyright and Licensing

**Key concerns:**
- AI-generated code may resemble copyrighted code
- Unclear legal status of AI-generated content
- License compatibility issues
- Potential copyright infringement

**Best practices:**
- Understand your organization's AI usage policies
- Check licenses of suggested dependencies
- Document AI usage for legal compliance
- Consult legal counsel for commercial projects

### Privacy and Data Protection

**Considerations:**
- Code sent to AI services may be stored
- Proprietary algorithms might be leaked
- Sensitive data in code could be exposed
- Compliance with GDPR, HIPAA, etc.

**Mitigation:**
- Use local AI models for sensitive code
- Anonymize data in examples sent to AI
- Review AI service terms of service
- Follow organizational data policies

### Professional Ethics

**Ethical obligations:**
- Honesty about AI use (academic, professional)
- Not claiming AI-generated work as entirely your own
- Ensuring code quality and safety
- Considering societal impact of your code

## Conclusion

AI coding assistants are powerful tools that can enhance productivity, but they come with significant responsibilities. Success requires:

1. **Awareness** of what can go wrong
2. **Responsibility** for all code you commit
3. **Judgment** about when AI is appropriate
4. **Verification** of all AI suggestions
5. **Balance** between AI assistance and skill development
6. **Ethics** in how you use and disclose AI usage

::::::::::::::::::::::::::::::::::::: callout

### Remember

AI is a tool, not a replacement for human expertise, judgment, and responsibility. Use it wisely, verify everything, and never stop learning.

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints 

- AI can generate incorrect, insecure, or inefficient code - always verify
- You are fully responsible for all code you commit, regardless of AI involvement
- AI usage is inappropriate for critical systems, novel algorithms, and learning fundamentals
- Heavy AI reliance can lead to skill atrophy and reduced code understanding
- LLMs produce wrong code because they pattern-match rather than understand
- Comprehensive testing, code review, and iterative refinement are essential
- Balance AI productivity gains with maintaining your programming skills
- Consider legal, ethical, and privacy implications of AI tool usage
- Treat AI as a junior assistant requiring supervision, not an expert to trust blindly
- Responsible AI usage requires continuous learning and critical thinking

::::::::::::::::::::::::::::::::::::::::::::::::
