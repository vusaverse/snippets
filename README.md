# Snippets for RStudio

Custom snippets designed for RStudio.

Copy the snippets into the correct language file from the `Tools > Edit Code Snippets`.

Or use the following script to do it in R:

*Note: * This will append the snippets to your existing R snippets.


```
remotes::install_github("vusaverse/vusa")
library(vusa)

# URL of the GitHub file
github_file_url <- "https://raw.githubusercontent.com/vusaverse/snippets/main/r.snippets"

# Path to the temporary file where we will save the downloaded content
temp_file_path <- fs::path_temp("r.snippets")

# Download the file from GitHub
downloaded_file_path <- vusa::download_github_file(github_file_url, temp_file_path)

# Read the contents of the downloaded file
downloaded_contents <- readLines(downloaded_file_path)

snippets_SA <- downloaded_contents %>%
  ## Trim whitespaces from the rightside, but keep tabs
  str_replace("[ \r\n]+$", "")

# read in the first file and split it into chunks
file2_chunks <- split_file(temp_file_path)

# read in the second file and split it into chunks
file1_chunks <- split_file(vusa::get_snippets_file(type = "r"))


# find the chunks in file2 that are not in file1
diff_chunks <- setdiff(lapply(file2_chunks, paste, collapse="\n"), lapply(file1_chunks, paste, collapse="\n"))

# append the missing chunks to file1
if (length(diff_chunks) > 0) {
  file1 <- readLines(get_snippets_file(type = "r"))
  file1[length(file1) + 1] <- ""
  file1[length(file1) + 1] <- paste(diff_chunks, collapse="\n\n")
  writeLines(file1, get_snippets_file(type = "r"))
  message("Local snippet file has been edited.")
}

# Clean up the temporary file
file.remove(temp_file_path)

```
