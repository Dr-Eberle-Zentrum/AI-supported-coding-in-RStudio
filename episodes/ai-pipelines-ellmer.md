---
title: "Using AI within Pipelines via ellmer"
teaching: 30
exercises: 20
---

:::::::::::::::::::::::::::::::::::::: questions 

- What is `ellmer` and how does it integrate with AI models?
- How can I set up `ellmer` with GitHub Copilot in RStudio?
- How can I use AI prompts to process data within my analysis pipelines?
- What are the best practices for integrating AI into data processing workflows?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Understand the `ellmer` package and its capabilities
- Install and configure `ellmer` for use with AI models
- Integrate AI prompts into data processing pipelines
- Apply AI-powered transformations to datasets
- Develop reproducible AI-enhanced workflows

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction

The `ellmer` package provides a powerful interface for integrating large language models (LLMs) into R workflows. This enables you to leverage AI capabilities directly within your data processing pipelines, combining traditional statistical computing with modern AI assistance.

## What is ellmer?

`ellmer` is an R package that provides a unified interface to various LLM providers, including:

- GitHub Copilot (via GitHub Models)
- OpenAI models
- Anthropic Claude
- Google Gemini
- Local models via Ollama

It allows you to:

- Send prompts to AI models from R code
- Process text data with AI assistance
- Generate structured outputs
- Stream responses for interactive applications

::::::::::::::::::::::::::::::::::::: callout

### Why Use ellmer?

- **Unified API**: Work with different AI providers using consistent syntax
- **Pipeline Integration**: Seamlessly incorporate AI into tidyverse workflows
- **Reproducible**: Track prompts and model versions for reproducible research
- **Flexible**: Switch between models without rewriting code

::::::::::::::::::::::::::::::::::::::::::::::::

## Installing ellmer

First, install the `ellmer` package from CRAN or GitHub:

```r
# Install from CRAN
install.packages("ellmer")

# Or install development version from GitHub
# install.packages("remotes")
remotes::install_github("tidyverse/ellmer")
```

Load the package:

```r
library(ellmer)
library(tidyverse)  # For data manipulation
```

## Setting Up ellmer with GitHub Copilot

To use `ellmer` with GitHub Copilot (via GitHub Models), you need to set up authentication.


### Step 1-pat: Getting Access to GitHub Models

Given that we have already *registered our GitHub account in RStudio*, to use the 
GitHub Copilot features, we can **proceed to use the GitHub Models via `ellmer` without further actions**.



### Step 1-explicit: Get a GitHub Token and Store It Securely

**The following steps are only needed, if you have not already set up GitHub authentication in RStudio.**

1. Go to [github.com/settings/tokens](https://github.com/settings/tokens)
2. Click "Generate new token" → "Generate new token (classic)"
3. Give it a descriptive name (e.g., "ellmer-access")
4. Select the required scopes (typically `repo` and `user`)
5. Click "Generate token" and copy it immediately

Store your token securely in your R environment:

```r
# Option 1: Set for the current session
Sys.setenv(GITHUB_TOKEN = "your-token-here")

# Option 2: Store permanently in .Renviron
usethis::edit_r_environ()
# Add this line: GITHUB_TOKEN=your-token-here
# Save and restart R
```

::::::::::::::::::::::::::::::::::::: callout

### Security Best Practice

Never commit tokens or API keys to your code! Always use environment variables and add `.Renviron` to your `.gitignore` file.

::::::::::::::::::::::::::::::::::::::::::::::::

### Step 2: Initialize a Chat Object

```r
# Create a chat session with GitHub Copilot
chat <- chat_github()  # the used default model will be printed

# Test the connection
chat$chat("Hi, please give me a joke!")
```

::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 1: Setup and Test `ellmer`

1. Install the `ellmer` package
2. Create a chat object and send a test message
3. Verify you receive a response and enjoy your joke..
4. What do you see, when you print your `chat` object?

:::::::::::::::::::::::: solution 

## Solution

Printing the `chat` object shows 

- the model being used
- the number of tokens sent and received
- the total cost incurred (if applicable)
- the history of messages exchanged

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

## Using AI for Data Processing

### Basic Text Processing

Process individual text strings with AI:

```r
# Classify sentiment
texts <- c(
  "I love this product!",
  "This is terrible.",
  "It's okay, not great."
)

# Use AI to classify sentiment
chat <- chat_github()
# iterative call of chat interface using sapply() or purrr::map()
results <- purrr::map_chr(texts, 
  function(text) {
    chat$chat(paste("Classify the sentiment (positive/negative/neutral):", text))
  })
```

### Processing Data in Pipelines

Integrate AI into tidyverse pipelines:

```r
# Example: Customer feedback analysis
feedback_data <- tibble(
  id = 1:5,
  comment = c(
    "Great service, very helpful!",
    "Long wait times, not happy.",
    "Average experience.",
    "Excellent quality and fast delivery!",
    "Product arrived damaged."
  )
)

# Add AI-powered sentiment analysis
feedback_processed <- feedback_data %>%
  rowwise() %>% # ensures each row/information is processed individually
  mutate(
    sentiment = chat$chat(
      paste("Classify as positive/negative/neutral:", comment)
    ),
    key_themes = chat$chat(
      paste("Extract main themes (max 3 words):", comment)
    )
  )
```

### Aggregated calls to reduce IO

So far, one chat call was made per row.
An alternative is to aggregate multiple inputs into a single prompt, reducing the number of API calls:

```r
feedback_data |> 
  mutate(
    mood = 
      comment |> 
      str_c(collapse="#") |> 
      chat_high$chat( "Assign to each product feedback answer (provided as #-separated list) a respective category from (happy,unhappy) in a #-separated aggregated text output",
                      echo = "none") |> 
      str_split_1("#")
  )
```

That way, only one API call is made for the entire dataset.



::::::::::::::::::::::::::::::::::::: callout

### Rate Limits and Costs

Be aware of:

- API rate limits for your chosen provider (limited number of requests per minute/hour)
- Limited token quotas and prompt sizes
- Potential costs for API calls
- Processing time for large datasets
- Consider batching requests when possible (less tokens spent)

::::::::::::::::::::::::::::::::::::::::::::::::

### Advanced: Structured Output Generation

Request structured data from AI models:

```r
# Extract structured information
extract_info <- function(text) {
  prompt <- paste0(
    "Extract the following from this text and return as JSON:\n",
    "- sentiment (positive/negative/neutral)\n",
    "- urgency (high/medium/low)\n",
    "- category (product/service/delivery/other)\n\n",
    "Text: ", text
  )
  
  chat$chat(prompt)
}

# Apply to dataset
feedback_structured <- feedback_data %>%
  rowwise() %>%
  mutate(analysis = extract_info(comment))
```

::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 2: Build a Data Processing Pipeline

Create a tidyverse pipeline that:

1. creates a `tibble` dataset (columns `review_id` and `text`) with the following product reviews
  - *The software is intuitive but lacks some features. Rating: 4/5*
  - *Terrible experience, crashed multiple times. Very disappointed.*
  - *Perfect for my needs! Easy to use and fast. Highly recommend.*
2. Uses AI to classify the main topic of each review in up to two words
3. Extracts a numerical satisfaction score (1-5) from the text

:::::::::::::::::::::::: solution 

## Example Solution

```r
library(ellmer)
library(tidyverse)

# Sample data
reviews <- tibble(
  review_id = 1:3,
  text = c(
    "The software is intuitive but lacks some features. Rating: 4/5",
    "Terrible experience, crashed multiple times. Very disappointed.",
    "Perfect for my needs! Easy to use and fast. Highly recommend."
  )
)

# Initialize chat
chat <- chat_github()

# Process with AI
reviews %>%
  rowwise() %>%
  mutate(
    topic = chat$chat(paste("Main topic (1-2 words):", text)),
    score = chat$chat(paste("Satisfaction score 1-5:", text)),
  ) %>%
  ungroup()
```

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

## Best Practices for AI in Pipelines

### 1. Design Clear Prompts

```r
# Good: Specific and constrained
prompt <- "Classify sentiment as: positive, negative, or neutral. 
          Return only one word."

# Less effective: Vague
prompt <- "What do you think about this?"
```

### 2. Handle Errors Gracefully

```r
safe_chat <- function(chat, prompt) {
  tryCatch(
    chat$chat(prompt),
    error = function(e) {
      warning("API call failed: ", e$message)
      return(NA)
    }
  )
}

# Use in pipeline
data %>%
  mutate(ai_result = safe_chat(chat, prompt))
```

### 3. Cache Results

```r
# Save processed results to avoid reprocessing
processed_data <- data %>%
  mutate(ai_field = process_with_ai(text))

# Save to disk
write_rds(processed_data, "cache/processed_data.rds")

# Load cached version later
processed_data <- read_rds("cache/processed_data.rds")
```

### 4. Use Batch Processing for Large Datasets

```r
# Process in chunks to manage rate limits
process_in_batches <- function(data, batch_size = 10) {
  data %>%
    mutate(batch = ceiling(row_number() / batch_size)) %>%
    group_by(batch) %>%
    mutate(ai_result = process_with_ai(text)) %>%
    ungroup() %>%
    select(-batch)
}
```

This approach is especially useful for large datasets to avoid hitting API rate limits.

Furthermore, it can be nicely combined with the "aggregated calls" approach shown earlier.


## Reproducibility Considerations

Document your AI pipeline for reproducibility:

```r
# Initialize chat
chat <- chat_github()

# Record model and version
metadata <- list(
  model = chat$get_model(),
  provider = "github",
  date = Sys.Date(),
  ellmer_version = packageVersion("ellmer"),
  prompt_template = "Classify sentiment: {text}"
)

# Save with results
list(
  data = processed_data,
  metadata = metadata
) %>%
  write_rds("results_with_metadata.rds")
```

::::::::::::::::::::::::::::::::::::: discussion

### Group Discussion

Consider the following questions for discussion within the class:

- What types of data processing tasks in your work could benefit from AI integration?
- How would you balance reproducibility with using AI models that may change over time?
- What ethical considerations arise when using AI to process data?
- How do you validate the quality of AI-generated classifications or summaries?

:::::::::::::::::::::::::::::::::::::::::::::::::::

## Real-World Use Cases

### Text Classification

```r
# Categorize research abstracts
abstracts %>%
  mutate(field = chat$chat(
    paste("Research field (one word):", abstract)
  ))
```

### Data Cleaning

```r
# Standardize inconsistent entries
messy_data %>%
  mutate(cleaned = chat$chat(
    paste("Standardize company name:", company_name_raw)
  ))
```

### Content Generation

```r
# Generate descriptions
products %>%
  mutate(description = chat$chat(
    paste("Write 20-word product description for:", product_name)
  ))
```

### Translation and Localization

```r
# Translate content
content %>%
  mutate(translated = chat$chat(
    paste("Translate to Spanish:", english_text)
  ))
```

::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 3: Implement a Complete Workflow

Choose a scenario and implement a complete AI-enhanced pipeline:

- **Option A**: Analyze a dataset of tweets/social media posts
- **Option B**: Process customer support tickets
- **Option C**: Categorize research papers by topic

Include error handling, caching, and metadata tracking.

:::::::::::::::::::::::: solution 

## Example for Option B: Support Tickets

```r
library(ellmer)
library(tidyverse)

# Initialize
chat <- chat_github()

# Process tickets
process_ticket <- function(ticket_text) {
  list(
    category = safe_chat(chat, 
      paste("Category (billing/technical/account):", ticket_text)),
    priority = safe_chat(chat,
      paste("Priority (high/medium/low):", ticket_text)),
    suggested_response = safe_chat(chat,
      paste("Suggest 2-sentence response:", ticket_text))
  )
}

# Apply to dataset
tickets_processed <- tickets %>%
  rowwise() %>%
  mutate(analysis = list(process_ticket(description))) %>%
  unnest_wider(analysis)

# Save with metadata
output <- list(
  data = tickets_processed,
  metadata = list(
    processed = Sys.time(),
    model = chat$get_model(),
    n_tickets = nrow(tickets)
  )
)

write_rds(output, "processed_tickets.rds")
```

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

## Troubleshooting Common Issues

### Authentication Errors

- Verify your token is set correctly: 
  - `Sys.getenv("GITHUB_PAT_GITHUB_COM")` for RStudio setup
  - `Sys.getenv("GITHUB_TOKEN")` for explicit token setup from above
- Ensure token has required permissions
- Check token hasn't expired

### Rate Limiting

- Implement delays between requests: `Sys.sleep(1)`
- Use batch processing
- Consider caching results
- Monitor API usage

### Inconsistent Results

- Make prompts more specific
- Add constraints to expected outputs
- Use [temperature parameter](https://www.vellum.ai/llm-parameters/temperature) (if supported)
- Validate and clean AI outputs

## Future Developments

Stay updated with `ellmer` developments:

- New model integrations
- Enhanced streaming capabilities
- Better error handling
- Performance improvements

Check the [ellmer documentation](https://ellmer.tidyverse.org) regularly for updates.

::::::::::::::::::::::::::::::::::::: keypoints 

- `ellmer` provides a unified interface for integrating LLMs into R workflows
- Set up authentication using environment variables for security
- Integrate AI prompts seamlessly into tidyverse pipelines
- Design clear, constrained prompts for consistent results
- Implement error handling and caching for robust pipelines
- Document models and prompts for reproducibility
- Consider rate limits, costs, and ethical implications when using AI in data processing

::::::::::::::::::::::::::::::::::::::::::::::::
