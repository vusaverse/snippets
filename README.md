# Snippets for RStudio

Various custom snippets designed for RStudio.

Copy the snippets into the correct language file from the `Tools > Edit Code Snippets`.

Or use [dgrtwo/snippr](https://github.com/dgrtwo/snippr) to install:


```
# remotes::install_github("dgrtwo/snippr")
library(snippr)

# For all snippets
snippets_install_github("vusaverse/snippets")

# For just the R snippets
snippets_install_github("vusaverse/snippets", language = "r")

# For just an individual snippet
snippets_install_github("vusaverse/snippets", language = "r", name = "aa")

```
