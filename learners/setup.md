---
title: Setup
---

This lesson introduces AI-supported coding tools in RStudio, specifically focusing on GitHub Copilot and other AI assistants. To participate in this lesson, you will need to set up the required software and accounts.

## Software Requirements

### R

You will need a recent version of R installed on your computer. We recommend:

- **R version 4.0.0 or later**

Download R from [CRAN](https://cran.r-project.org/).

### RStudio

You will need a recent version of RStudio with GitHub Copilot support:

- **RStudio version 2022.02 or later** (required for GitHub Copilot integration)

Download RStudio from [Posit](https://posit.co/download/rstudio-desktop/).

::::::::::::::::::::::::::::::::::::: callout

### Why RStudio 2022.02 or later?

GitHub Copilot integration in RStudio was introduced in version 2022.02. Earlier versions do not support the Copilot extension, which is essential for this lesson.

::::::::::::::::::::::::::::::::::::::::::::::::

## GitHub Account (Required)

**A GitHub account is essential for this lesson** as GitHub Copilot requires authentication through GitHub.

If you don't already have a GitHub account:

1. Go to [github.com](https://github.com)
2. Click "Sign up" and follow the registration process
3. **Tip:** Use your university or institutional email address to make it easier to apply for student benefits

::::::::::::::::::::::::::::::::::::: callout

### GitHub Student Developer Pack

Students can get **free access to GitHub Copilot** through the GitHub Student Developer Pack. This includes:

- Free GitHub Copilot subscription
- Access to other premium development tools
- Cloud credits and educational resources

We recommend applying for the Student Developer Pack before the lesson. The application process is covered in detail in the [Getting Started with GitHub Copilot](episodes/getting-started-with-copilot.md) chapter, but you can start the process early at [education.github.com/pack](https://education.github.com/pack).

**Note:** Application approval typically takes a few days, so please apply in advance if possible.

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

The `ellmer` package provides interfaces to various AI models directly from R. While this is covered in detail in a later chapter, having it pre-installed will save time during the lesson.

::::::::::::::::::::::::::::::::::::::::::::::::

## Setup Verification

Before the lesson begins, verify your setup:

1. **Check R version:**
   ```r
   R.version.string
   ```
   Should show R version 4.0.0 or later.

2. **Check RStudio version:**
   - Open RStudio
   - Go to `Help` → `About RStudio`
   - Verify the version is 2022.02 or later

3. **Verify GitHub account:**
   - Ensure you can log in at [github.com](https://github.com)
   - Check if you have applied for the Student Developer Pack (if applicable)

## Getting Help

If you encounter issues with setup:

- Check the [Getting Started with GitHub Copilot](episodes/getting-started-with-copilot.md) chapter for detailed GitHub Copilot setup instructions
- Refer to the [RStudio documentation](https://docs.posit.co/ide/user/) for RStudio-specific questions
- Contact the instructors before the lesson if you have persistent setup problems

## What's Next?

Once your setup is complete, you're ready to start the lesson! The first chapter, [Getting Started with GitHub Copilot](episodes/getting-started-with-copilot.md), will guide you through:

- Registering for GitHub (if you haven't already)
- Applying for the GitHub Student Developer Pack
- Installing and configuring GitHub Copilot in RStudio
- Testing that everything works correctly

We look forward to exploring AI-supported coding with you!

