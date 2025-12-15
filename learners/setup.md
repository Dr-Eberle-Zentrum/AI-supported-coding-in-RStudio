---
title: Setup
---

# Setup

This lesson introduces AI-supported coding tools in RStudio, specifically focusing on GitHub Copilot and other AI assistants. 
To participate in this lesson, you will need to set up the required software and accounts.

## Software Requirements

### R

You will need a recent version of R installed on your computer. We recommend:

- **R version 4.2.0 or later**

Download R from [CRAN](https://cran.r-project.org/).

### RStudio

You will need a recent version of RStudio with GitHub Copilot support:

- **RStudio version 2024.02 or later** (required for GitHub Copilot integration)

Download RStudio from [Posit](https://posit.co/download/rstudio-desktop/).

::::::::::::::::::::::::::::::::::::: callout

### Why RStudio 2022.02 or later?

GitHub Copilot integration in RStudio was introduced in version 2022.02. 
Earlier versions do not support the Copilot extension, which is essential for this lesson.

::::::::::::::::::::::::::::::::::::::::::::::::

## Optional: R Packages

Some chapters in this lesson use additional R packages. These will be introduced as needed during the lesson, but you may want to install them in advance:

```r
# For data manipulation (used in examples)
install.packages("tidyverse")

# For AI integration in pipelines (Chapter: Using AI within Pipelines)
install.packages("ellmer")
```

::::::::::::::::::::::::::::::::::::: callout

### About the ellmer Package

The `ellmer` package provides interfaces to various AI models directly from R. 
While this is covered in detail in a later chapter, having it pre-installed will save time during the lesson.

::::::::::::::::::::::::::::::::::::::::::::::::

## Setup Verification

Before the lesson begins, verify your setup:

1. **Check R version:**
   ```r
   R.version.string
   ```
   Should show R version 4.2.0 or later.

2. **Check RStudio version:**
   - Open RStudio
   - Go to `Help` → `About RStudio`
   - Verify the version is 2024.02 or later


## Getting Help

If you encounter issues with setup:

- Refer to the [RStudio documentation](https://docs.posit.co/ide/user/) for RStudio-specific questions
- Contact the instructors before the lesson if you have persistent setup problems

## What's Next?

Once your setup is complete, you're ready to start the lesson! 
The first chapter, [Getting Started with GitHub Copilot](episodes/getting-started-with-copilot.md), will guide you through:

- Registering for GitHub (if you haven't already)
- Applying for the GitHub Student Developer Pack
- Installing and configuring GitHub Copilot in RStudio
- Testing that everything works correctly

We look forward to exploring AI-supported coding with you!

