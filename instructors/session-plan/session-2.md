
# Session 2


## Required Self-Study

- [Risks, Drawbacks and Responsibilities with AI Usage](../../episodes/ai-risks-responsibilities.html)
- [RStudio Autocompletion with Copilot](../../episodes/rstudio-autocompletion.html)



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
