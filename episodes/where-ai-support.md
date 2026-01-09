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
- Writing function documentation in [roxygen2 format](https://roxygen2.r-lib.org/index.html)
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
- Explain function parameters and usage or given code
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

Remember that code sent to AI services may be used for training. 

**Never include:**

- API keys or passwords
- Proprietary algorithms/code
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

1. Does this code produce valid results?
2. Are the assumptions appropriate for my data?
3. Does it handle missing data correctly?
4. Are there edge cases that aren't covered?
5. Is this the most efficient approach?
6. Does it align with best practices in my field?

*Keep asking/investigating until you can confidently answer "yes" to all questions!*

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

## Developing a Balanced Approach

### Best Practices for Using AI Assistants

1. **Start with a clear goal:** Know what you want to achieve before asking for AI help
   - Best decompose complex tasks into smaller, manageable parts that can be easily checked
2. **Review and understand:** Never accept suggestions blindly
   - Request explanations for AI-generated code until you understand it fully
3. **Test thoroughly:** Validate all AI-generated code
   - Think about "What can go wrong?" (edge cases) and design tests accordingly
4. **Iterate and refine:** Use AI suggestions as a starting point, not the final solution
   - Often AI helps with code fragments. Do/request a final revision to merge them into a coherent whole
5. **Maintain ownership:** You are responsible for the code in your project
   - Ensure it meets your project's standards and requirements

### When to Rely on Human Expertise

Prioritize human judgment for:

- Critical decision-making about architecture and design
- Code review and quality assessment
- Understanding domain-specific requirements
- Ethical considerations in code implementation
- Debugging complex issues




## Ways How AI Assistance Can Help You

Typically, one distinguishes between three **ways of AI usage**:

| Assistively | Directively | Autonomously |
|-------------|-------------|--------------|
| ![](ai-mode-1.png) | ![](ai-mode-2.png) | ![](ai-mode-3.png) |
| AI suggests code snippets, completes lines, or generates boilerplate code automatically. | AI generates larger code blocks or entire functions based on explicit prompts. | AI independently creates code with minimal human input based on high-level requirements. |
| This is typically done automatically without the need to explicitly ask for it. | Here, you explicitly ask the AI to perform a specific task. | You provide high-level requirements or a description of a larger task, and the AI generates the code accordingly. |



Within this course, we will investigate all three ways of AI usage.

## What is Supported by AI?

Beside the way *how* AI is used, one can also distinguish *what process is supported* by AI:

- **Coding Support**
  - AI assists with writing and revising your code
  - i.e. AI is used as a tool within your coding workflow
  - this can be done as a code assistant or as a code generator
  - subtasks are e.g. 
    - **syntax support**: AI helps with code syntax, such as completing function calls, correcting errors, or suggesting variable names.
    - **logic support**: AI assists with the logical structure of the code, such as suggesting algorithms, data structures, or control flow.
    - **documentation support**: AI helps with writing comments, documentation, or explanations for the code.
    - **debugging support**: AI assists in identifying and fixing bugs, suggesting test cases, or improving code quality.
    - **optimization support**: AI helps improve code performance, suggesting optimizations, refactoring, or resource management techniques.
- **Data Processing Support**: AI assists in cleaning, transforming, and preparing data for analysis.
  - i.e. AI is used as a tool within data processing pipelines.
  - e.g. we will use the `ellmer` R package later in this course for AI-supported data generation.
- **Project Management Support**
  - AI aids in organizing tasks, tracking progress, and managing timelines.
  - i.e. AI is used as a tool within project management software
  - e.g. GitHub Copilot Codespaces, GitHub Issues AI, etc.
- **Collaboration Support**
  - AI facilitates teamwork by suggesting code reviews, merging changes, or managing version control.
  - e.g. GitHub Copilot Chat, GitHub Pull Requests AI, etc.
- **Learning Support**
  - AI provides educational assistance, such as explaining concepts, suggesting resources, or guiding through coding challenges.  
  - typically using a chatbot interface
  - e.g. ChatGPT, GitHub Copilot Chat, etc.
- ... something missing?! Let us know!


::::::::::::::::::::::::::::::::::::: discussion

### Preparation of Group Discussion

In small groups, we want to discuss:

- Have you used AI coding assistants before? What was your experience?
- Can you share an example where AI helped you solve a problem?
- Can you share an example where AI suggestions were incorrect or unhelpful?
- How do you decide when to use AI assistance versus figuring things out yourself?

Thus, please think on these questions for our upcoming group discussion.

:::::::::::::::::::::::::::::::::::::::::::::::::::

## The Future of AI in Coding

AI assistants are rapidly evolving. As they improve, we should:

- Stay informed about new capabilities and limitations
- Continuously refine our approach to using these tools
- Share knowledge about effective practices
- Contribute to discussions about responsible AI use



::::::::::::::::::::::::::::::::::::: keypoints 

- AI assistants excel at generating boilerplate code, completing syntax, and helping with documentation
- Use caution with complex logic, project-specific requirements, and security-critical code
- Always review and test AI-generated code thoroughly
- AI assistants are tools to augment, not replace, human expertise
- Develop a balanced approach that leverages AI strengths while maintaining code quality and security
- Stay open to learning and adapting as AI technologies evolve

::::::::::::::::::::::::::::::::::::::::::::::::



::::::: instructor

[Plan for Session 1](../instructors/session-1.md)

::::::::::::::::::


