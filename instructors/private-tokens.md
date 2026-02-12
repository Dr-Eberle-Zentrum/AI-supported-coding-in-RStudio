

## Avoiding GitHub Copilot from Reading Secrets in RStudio

Because GitHub Copilot works by sending snippets of your current code to a server to generate suggestions, the only foolproof way to keep secrets out of Copilot is to never type them directly into your R scripts.

Instead of hardcoding credentials, you should use an environment variable approach. This keeps your secrets in a separate file that Copilot doesn't process for suggestions.

Here are the best practices for managing this in RStudio.

### 1. Store Credentials in `.Renviron`

The `.Renviron` file is a special configuration file loaded when R starts. It is the standard place to store API keys, database passwords, and tokens.

#### (I) In RStudio, type the following command in your console:

```
  usethis::edit_r_environ()

  A new file named `.Renviron` will open. Add your credentials in KEY=VALUE format:
  Plaintext

  DATABASE_PASSWORD=your_actual_password_here
  API_TOKEN=your_actual_token_here
```

Save the file and restart your R session (Session -> Restart R) for the changes to take effect.

#### (II) Reference Variables in Your Code

Now, in your R script, instead of typing the password, you call the environment variable. 
Copilot will only see the variable name (`Sys.getenv(...)`), not the actual secret.

Instead of this (BAD):

```
con <- dbConnect(PostgreSQL(), password = "supersecretpassword123")
```

Do this (GOOD):

```
# Copilot sees this, which is safe
con <- dbConnect(PostgreSQL(), password = Sys.getenv("DATABASE_PASSWORD"))
```

#### (III) Set the Variables via Operating System (Advanced)

While Copilot in RStudio is primarily focused on the active file, it sometimes scans nearby files to understand project context. 
To prevent it from reading files containing secrets you can store your credentials in environment variables at the operating system level instead of using `.Renviron`.

- **Windows**: Use the System Properties -> Environment Variables to set your variables.
- **macOS/Linux**: Add export statements to your shell profile (e.g., `~/.bash_profile` or `~/.zshrc`):

