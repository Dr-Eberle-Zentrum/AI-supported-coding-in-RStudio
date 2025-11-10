---
title: "Getting Started with GitHub Copilot"
teaching: 20
exercises: 10
---

:::::::::::::::::::::::::::::::::::::: questions 

- How do I register for a GitHub account?
- How can I get free GitHub Copilot access as a student?
- How do I set up GitHub Copilot in RStudio?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Create a GitHub account
- Apply for GitHub Student Developer Pack
- Install and configure GitHub Copilot in RStudio
- Verify GitHub Copilot is working as an autocompletion tool

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction

GitHub Copilot is an AI-powered code completion tool that can significantly enhance your coding experience in RStudio. This chapter will guide you through the process of setting up GitHub Copilot, from creating a GitHub account to configuring it in RStudio.

## Registering with GitHub

If you don't already have a GitHub account, follow these steps:

1. Navigate to [github.com](https://github.com)
2. Click the "Sign up" button in the top right corner
3. Enter your email address (preferably your university/institutional email)
4. Create a strong password
5. Choose a username
6. Verify your account through the email confirmation

::::::::::::::::::::::::::::::::::::: callout

### Why use your university email?

Using your university or institutional email address makes it easier to verify your student status when applying for the GitHub Student Developer Pack.

::::::::::::::::::::::::::::::::::::::::::::::::

## Requesting GitHub Student Developer Pack

GitHub offers free access to GitHub Copilot and other premium features to students through the GitHub Student Developer Pack.

### Steps to Apply

1. Go to [education.github.com/pack](https://education.github.com/pack)
2. Click on "Sign up for Student Developer Pack"
3. Sign in with your GitHub account if not already logged in
4. Fill out the application form:
   - Select your school from the dropdown (or enter it manually)
   - Provide your school-issued email address
   - Describe how you plan to use GitHub (e.g., "For coursework and research projects")
5. Upload proof of enrollment:
   - Student ID card
   - Official enrollment letter
   - Transcript or other academic document
6. Submit your application

::::::::::::::::::::::::::::::::::::: callout

### Application Processing Time

GitHub typically processes student applications within a few days, but it can take up to 2 weeks. You'll receive an email notification once your application is approved.

::::::::::::::::::::::::::::::::::::::::::::::::

## Installing GitHub Copilot in RStudio

Once your GitHub Student Developer Pack is approved, you can set up GitHub Copilot in RStudio.

### Prerequisites

- RStudio version 2022.02 or later
- GitHub account with Copilot access

### Installation Steps

1. **Install the GitHub Copilot extension in RStudio:**
   - Open RStudio
   - Go to `Tools` → `Global Options`
   - Select `Copilot` from the left sidebar
   - Click "Enable GitHub Copilot"
   - If the Copilot option is not available, make sure you're running RStudio 2022.02 or later

2. **Sign in to GitHub:**
   - Click "Sign in to GitHub" in the Copilot settings
   - A browser window will open asking you to authorize RStudio
   - Click "Authorize" to grant RStudio access to your GitHub account
   - You may be asked to enter a device code - copy the code shown in RStudio and paste it into the browser

3. **Verify the connection:**
   - Return to RStudio
   - You should see a confirmation that GitHub Copilot is enabled
   - The status should show "GitHub Copilot: Active"

::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 1: Test GitHub Copilot

Open a new R script in RStudio and try typing a comment describing a function, such as:

```r
# Function to calculate the mean of a numeric vector
```

Does GitHub Copilot suggest a function implementation?

:::::::::::::::::::::::: solution 

## Solution

GitHub Copilot should suggest a function implementation below your comment. The suggestion might look something like:

```r
# Function to calculate the mean of a numeric vector
calculate_mean <- function(x) {
  sum(x) / length(x)
}
```

You can accept the suggestion by pressing `Tab` or continue typing to see alternative suggestions.

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

## Configuring Copilot Settings

You can customize how GitHub Copilot works in RStudio:

1. Go to `Tools` → `Global Options` → `Copilot`
2. Adjust settings such as:
   - **Enable/Disable Copilot:** Toggle Copilot on or off
   - **Suggestion mode:** Configure how suggestions appear
   - **Keybindings:** Customize keyboard shortcuts for accepting suggestions

::::::::::::::::::::::::::::::::::::: callout

### Tips for Using Copilot

- Write clear, descriptive comments to get better suggestions
- Review all suggestions before accepting them
- Use Tab to accept a suggestion, or Esc to dismiss it
- Copilot learns from context, so well-structured code gets better suggestions

::::::::::::::::::::::::::::::::::::::::::::::::

## Troubleshooting Common Issues

### Copilot is not showing suggestions

- Verify that Copilot is enabled in settings
- Check that you're signed in to GitHub
- Ensure your GitHub Copilot subscription is active
- Try restarting RStudio

### Authorization fails

- Clear your browser cache and try again
- Make sure you're using the correct GitHub account
- Check that your GitHub Copilot access is active

::::::::::::::::::::::::::::::::::::: keypoints 

- A GitHub account is required to use GitHub Copilot
- Students can get free GitHub Copilot access through the GitHub Student Developer Pack
- GitHub Copilot integrates directly into RStudio as an autocompletion tool
- Test Copilot by writing descriptive comments and observing the suggestions
- Copilot can be customized through RStudio's settings

::::::::::::::::::::::::::::::::::::::::::::::::
