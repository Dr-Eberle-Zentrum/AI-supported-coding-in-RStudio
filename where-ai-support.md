---
title: "Where Do We Need AI Support?"
teaching: 15
exercises: 10
---

:::::::::::::::::::::::::::::::::::::: questions 

- What types of coding tasks can benefit from AI assistance?
- When should we use AI coding assistants and when shouldn't we?
- What are the limitations of AI-powered coding tools?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Identify scenarios where AI coding assistants are most helpful
- Understand the limitations and potential pitfalls of AI-generated code
- Develop a balanced approach to using AI in coding workflows
- Recognize when human expertise is essential

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction

AI-powered coding assistants like GitHub Copilot have revolutionized how we write code, 
but understanding when and how to use them effectively is crucial. 
This chapter explores the scenarios where AI support is most beneficial and where caution is needed.

## Scenarios Where AI Assistants Excel

### 1. Boilerplate Code Generation

AI assistants are particularly effective at generating repetitive, standard code patterns:

- Function templates and class structures
- Data validation checks
- Common data transformations
- Standard file I/O operations

::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 1: Identify Boilerplate Code

Think about your recent coding projects. 
List 2-3 examples of repetitive code patterns you frequently write that could benefit from AI assistance.

:::::::::::::::::::::::: solution 

## Example Solutions

Examples might include:

- Reading CSV files and performing basic data cleaning
- Creating standard plotting functions with ggplot2
- Writing function documentation in roxygen2 format
- Setting up standard data frame transformations with dplyr

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

### 2. Code Completion and Syntax

AI can help with:

- Completing function arguments
- Suggesting appropriate function names from loaded packages
- Correcting syntax errors
- Providing context-aware variable names

### 3. Documentation and Comments

Writing clear documentation is time-consuming but essential. AI can assist with:

- Generating function documentation
- Creating informative code comments
- Writing README files
- Producing example usage code

### 4. Learning New Libraries and Functions

When working with unfamiliar packages or functions:

- AI can suggest appropriate functions for specific tasks
- Provide example implementations
- Offer alternative approaches

## Scenarios Requiring Caution

### 1. Complex Logic and Algorithms

AI assistants may struggle with:

- Domain-specific algorithms
- Complex statistical methods
- Unique business logic
- Performance-critical code

::::::::::::::::::::::::::::::::::::: callout

### Critical Review Required

Always carefully review AI-generated code for:

- Logical correctness
- Edge case handling
- Performance implications
- Security vulnerabilities

::::::::::::::::::::::::::::::::::::::::::::::::

### 2. Project-Specific Requirements

AI may not understand:

- Specific coding standards in your project
- Custom architectural patterns
- Project-specific constraints
- Team conventions and best practices

### 3. Data Privacy and Security

Be cautious when:

- Working with sensitive or proprietary data
- Implementing security-critical features
- Handling authentication and authorization
- Processing personal information

::::::::::::::::::::::::::::::::::::: callout

### Data Privacy Considerations

Remember that code sent to AI services may be used for training. Never include:

- API keys or passwords
- Proprietary algorithms
- Sensitive data
- Personal information

::::::::::::::::::::::::::::::::::::::::::::::::

## Limitations of AI Coding Assistants

### Understanding Context

- AI may miss broader project context
- Limited understanding of project history and evolution
- Cannot always infer implicit requirements

### Code Quality

- Generated code may not follow best practices
- Potential for introducing subtle bugs
- May suggest outdated or deprecated approaches

### Dependency on Training Data

- Biased toward common patterns seen in training data
- May not know about very recent updates or libraries
- Could suggest obsolete methods

::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 2: Evaluate AI Suggestions

Consider this scenario: You ask an AI assistant to generate code for a statistical analysis. 
What questions should you ask yourself before accepting the suggestion?

:::::::::::::::::::::::: solution 

## Questions to Consider

Before accepting AI-generated code, ask:

1. Does this code produce statistically valid results?
2. Are the assumptions appropriate for my data?
3. Does it handle missing data correctly?
4. Are there edge cases that aren't covered?
5. Is this the most efficient approach?
6. Does it align with best practices in my field?

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

## Developing a Balanced Approach

### Best Practices for Using AI Assistants

1. **Start with a clear goal:** Know what you want to achieve before asking for AI help
2. **Review and understand:** Never accept suggestions blindly
3. **Test thoroughly:** Validate all AI-generated code
4. **Iterate and refine:** Use AI suggestions as a starting point, not the final solution
5. **Maintain ownership:** You are responsible for the code in your project

### When to Rely on Human Expertise

Prioritize human judgment for:

- Critical decision-making about architecture and design
- Code review and quality assessment
- Understanding domain-specific requirements
- Ethical considerations in code implementation
- Debugging complex issues

::::::::::::::::::::::::::::::::::::: discussion

### Group Discussion

In small groups, discuss:

- Have you used AI coding assistants before? What was your experience?
- Can you share an example where AI helped you solve a problem?
- Can you share an example where AI suggestions were incorrect or unhelpful?
- How do you decide when to use AI assistance versus figuring things out yourself?

:::::::::::::::::::::::::::::::::::::::::::::::::::

## The Future of AI in Coding

AI assistants are rapidly evolving. As they improve, we should:

- Stay informed about new capabilities and limitations
- Continuously refine our approach to using these tools
- Share knowledge about effective practices with colleagues
- Contribute to discussions about responsible AI use in software development

::::::::::::::::::::::::::::::::::::: keypoints 

- AI assistants excel at generating boilerplate code, completing syntax, and helping with documentation
- Use caution with complex logic, project-specific requirements, and security-critical code
- Always review and test AI-generated code thoroughly
- AI assistants are tools to augment, not replace, human expertise
- Develop a balanced approach that leverages AI strengths while maintaining code quality and security

::::::::::::::::::::::::::::::::::::::::::::::::
