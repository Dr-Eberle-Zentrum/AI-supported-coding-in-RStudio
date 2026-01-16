

# Session 4


## Required Self-Study

- [Revise Your Code with AI](../episodes/revise-code-with-ai.md)
- [GitHub Issue-Driven Coding with Copilot](../episodes/github-issue-driven-coding.md)



## Session Plan

- ? How are you typically using AI tools in your coding workflow?
  - small code fragments
  - individual steps
- ? What issues arise from "localized" use of AI tools?
  - context switching
  - integration challenges
  - consistency issues

- code revision ... ? what are goals for code revision?
  - improve code quality
    - reduce redundancy (and number of temporary variables)
    - simplify logic and workflows
  - enhance readability
    - spacings, indention, ...
    - comments and documentation
  - ensure best practices
    - naming conventions
    - package usage

- AI is well suited to provide such a "holistic" code revision

### OPTION 1: chat-based revision

- upload existing code (file) for revision
- prompt engineering for code revision
  - "revise this code to improve readability and maintainability"
  - "optimize this code for performance without changing its functionality"
  - "add comments and documentation to this code"
- will produce revised code for download

- ? What are the advantages and disadvantages of chat-based code revision?
  - advantages
    - interactive feedback
    - tailored revisions
  - disadvantages
    - context limitations
    - potential for misinterpretation
    - lack of integration with development environment to compare changes

- **NOTE**: revision is typically a multi-step process
  - initial revision
  - review of revised code
  - further refinement requests
- can also be applied to revise code snippets to see alternative implementations

- **Do not settle for code you don't understand!** 
  - in that case ask to alternatives you are familiar with!
  - the final code is YOUR responsibility!

### OPTION 2: IDE-integrated revision

- use IDE AI plugin to revise code directly in the coding environment
  - either for full file
  - or for selected code blocks
- **PROBLEM**: RStudio does not yet have AI-integration... 😢
  - possible workaround: `chattr` package to connect to chat-based LLMs from RStudio
    - but no direct code revision support yet
    - personally: so far, I found it currently not very useful for code revision tasks

### OPTION 3: Issue-driven coding with Copilot

- ? What's a GitHub repository?
- ? Relation of GitHub repository and local project?
- ? What's the difference of a GitHub repository and cloud-space-shared project?

- ? Do you know git?
  - discussion of git workflow and basics

- ? what's a GitHub issue?
  - issue as "to-do" item
  - issue description as prompt for code generation
  - >> ! can be used to trigger autonomous code generation by Copilot !

- DEMO: based on an existing GitHub repository with issues defined

- ? What are the advantages and disadvantages of issue-driven coding with Copilot?
  - advantages
    - structured workflow
    - clear objectives
    - integration with version control
      - **visualize and track changes**
    - parallize workload by "recruiting AI assistants"
      - focus on high-level design, code revision and integration
  - disadvantages
    - learning curve for git and GitHub
    - potential for misalignment between issue description and generated code

- ? In which scenarios would issue-driven coding be most beneficial?

- TASK: 
  - ! create a GitHub repository for a small project (or use an existing one)!
  - ! use the example solution of ["Challenge 1" from the material](https://dr-eberle-zentrum.github.io/AI-supported-coding-in-RStudio/github-issue-driven-coding.html)
      as an initial issue to create the first R code file for your project
    - assign the issue to GitHub Copilot
    - review the generated code carefully!
    - if necessary, refine the issue description and try again!
    - merge/integrate the generated code into your project (closing the completed pull request)!
  - ! define at least 2 additional issues for the project, describing further tasks to be done!
    - coding (e.g. implementing a function, visualization, ... or writing equivalent code in another language))
    - revision (e.g. improving existing code, suggesting tests, ...)
    - documentation (e.g. updating/extending README.md or code commenting)
    - creating additional files (e.g. AGENTS.md)
    - ...
  - ! use Copilot to address each issue!
    - review the generated code carefully!
    - if necessary, refine the issue description and try again!
  - ! review and integrate the generated code into your project (merging the completed pull requests)!

### Closing Discussion

- Always check balance between effort needed to guide AI and expected benefits...
  - ... sometimes it's just faster to do it yourself!

- ? What are your key takeaways from this course?
  - ? Is/will AI-assisted coding be part of your workflow?


