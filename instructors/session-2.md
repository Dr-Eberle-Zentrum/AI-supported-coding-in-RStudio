
# Session 2


## Required Self-Study

- [Risks, Drawbacks and Responsibilities with AI Usage](../episodes/ai-risks-responsibilities.md)
- [RStudio Autocompletion with Copilot](../episodes/rstudio-autocompletion.md)
- [Context Definition and the AGENTS.md Concept](../episodes/context-definition-agents.md)



## Session Plan

### Autocompletion

- **Shortcut to switch Copilot on/off**
  - via "Command Palette": 
    - SHIFT+CTRL+P or SHIFT+COMMAND+P > type "Copilot"
  - setup of personal key combination
    - `Tools` > `Modify Keyboard Shortcuts..` 
    - use filter field with "Copilot" to find
      - `Copilot: Toggle Automatic Completion`
    - click into center column of the table to set your key combination
      - e.g. SHIFT+CTRL+ALT+P or whatever you like

- **Coding examples** ... to experience context dependency (comments)
  - enable Copilot and autocompletion
  - create **two** new R scripts
    - copy & paste the following code snippets into the two scripts
  - try to complete the code by accepting Copilot suggestions
    - compare the results!

```r
library(tidyverse)
data("storms")

# visualize for each year the maximal wind speed and the number of storms
# in a bar chart with two bars per year
```

```r
library(tidyverse)
data("storms")

# identify for each storm in each year the maximal wind speed
# visualize for each year the maximal wind speed of the strongest storm
# and the number of storms in a bar chart with two bars per year
# ensure that the year names on the x-axis are readable
```

- **Discuss within your group:**
  - ? do you see differences?
  - ? which code seems more appropriate/correct? 
  - ? do you understand all code elements?

- ! Context matters ... 

- ? **What happened to enable the code suggestions?**
  - Copilot uses the context of the current file
  - ! *requires upload of your code!*
  - ? drawbacks? (security, online traffic, energy consumption, bubble, ...)
    - ! use with care!

- **Setup of Copilot options**
  - `Tools` > `Global Options`
  - "Copilot" menu on the left
    - for most use cases: sufficient to disable indexing of whole project!

### Context Definition

- so far: **context via comments**
  - PRO: simple and quick to use
  - CON: general requirements and coding constraints need to be defined in each document
- alternative: **context via `AGENTS.md` files**
  - PRO: central definition of requirements and constraints for the whole project
  - CON: requires some setup and maintenance = additional work but WORTH IT!
  - typically requires code organisation in terms of **projects** (RStudio Projects)
  - **IMPORTANT: need to activate “Index project files with GitHub Copilot” in RStudio > Copilot options!**

- ? Who is familiar with **RStudio Projects**?
  - idea and setup
    - relation of project and working directory
    - relation of project and git repository
  - switching projects
  - `AGENTS.md` file
    - project root directory vs. subdirectory
    - verbose description of coding requirements and constraints
      - even more detailed than comments in code files
      - use examples
      - update regularly while working on the project

- **Exercise: Setup of RStudio Project with `AGENTS.md` file**
  - create a new RStudio Project
  - add a new R script with the short description from above
  - create an `AGENTS.md` file in the project root directory
    - provide detailed instructions for AI on general details on
      - coding style (e.g. where to put documenting comments)
      - visualization style (colors, fonts, themes, ...)
      - image generation (output file format, sizes, resolution, ...)
      - any other requirements or constraints you find important
    - ! *you might want to use AI-supported autocompletion for this...!*
  - reopen the created R script with the incomplete code
    - try to complete the code by accepting Copilot suggestions
  - compare the results with those from the previous exercise
  - double check your `AGENTS.md` file
    - ? did Copilot follow your instructions?
    - ? what could be improved in your `AGENTS.md` file?
      - too specific vs. too general?

