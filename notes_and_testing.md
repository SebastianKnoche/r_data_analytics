---
title: "Notes and testing"
subtitle: ""
author: "Sebastian Knoche"
date: "2021-05-27"
output:
  html_document:
    keep_md: yes
  pdf_document: default
---




# Install/update important packages


```r
install.packages(c(
  "dplyr",         # A Grammar of Data Manipulation
  "ggplot2",       # Create Elegant Data Visualisations Using the Grammar of Graphics
  "pracma",        # Practical Numerical Math Functions
  "rmarkdown",     # Dynamic Documents for R
  "wooldridge",    # 111 Data Sets from "Introductory Econometrics: A Modern Approach, 6e" by Jeffrey M. Wooldridge
  "gapminder",     # Data from Gapminder
  "ISLR",          # Data for an Introduction to Statistical Learning with Applications in R
# "nycflights13",  # Flights that Departed NYC in 2013
# "titanic",       # Titanic Passenger Survival Data Set
  "e1071",         # Misc Functions of the Department of Statistics, Probability Theory Group (Formerly: E1071), TU Wien
  "rstudioapi",    # Safely Access the RStudio API
  "xml2"           # Parse XML
  ))
```


# Changing RStudio themes

* download theme  

[wvictor14 - rstudio themes](https://github.com/wvictor14/rstudio_themes)  
[tmTheme editor](https://tmtheme-editor.herokuapp.com/#!/editor/theme/Multilanger%20Dark_inverted)  
[grubber theme](https://github.com/RobertMyles/grubber/blob/master/Grubber.rstheme)  
[gadenbuie - rsthemes](https://github.com/gadenbuie/rsthemes/tree/main/inst/themes)  

* install `rstudioapi` and `xml2` packages in RStudio  


```r
install.packages("rstudioapi")
install.packages("xml2")
```

* set the path


```r
# full path to the file - including file name
t_path <- "~/Documents/Uni/209002 Themenfeld (Gruppe 03)/r_themes/MultiLanger-Dark_Tweaked.tmTheme"
#t_path <- "~/Documents/Uni/209002 Themenfeld (Gruppe 03)/r_themes/49th Parallel.rstheme"
```

* convert and add `.tmTheme` file


```r
rstudioapi::convertTheme(t_path, add = TRUE, apply = TRUE)
```

* convert and add `.rstheme` file


```r
rstudioapi::addTheme(t_path, apply = TRUE)
```


# Experimentation with tables...

rechts|zentriert|zentriert|links
-:|-|:-:|:-
rechts|links|zentriert|links



# making the PDF and docx files


```r
filen <- "table" # name of my RMarkdown file without suffix
knit(paste0(filen,".Rmd"))

# make PDF
system(paste0("pandoc -s ", paste0(filen,".md"), " -t latex -o ", paste0(filen,".pdf"), " --highlight-style=tango  -S"))

# make docx
system(paste0("pandoc -s ", paste0(filen,".md"), " -o ", paste0(filen,".docx"), " --highlight-style=tango  -S"))
```

# URLs

[get RStudio](https://www.rstudio.com/products/rstudio/download)  
[datacamp courses](https://campus.datacamp.com/courses/)  
[datacarpentry](https://datacarpentry.org/R-genomics/01-intro-to-R.html)  
[Hinweise RStudio](https://moodle.hwr-berlin.de/pluginfile.php/1760685/mod_resource/content/2/hinweise_rstudio.html)  
[Titanic on kaggle](https://www.kaggle.com/alaasedeeq/predicting-the-survival-of-titanic-top-6?scriptVersionId=59514192)  
[swcarpentry](https://swcarpentry.github.io/r-novice-inflammation/02-func-R/)  
[setup git](https://cfss.uchicago.edu/setup/)  
[ggplot2 book](https://ggplot2-book.org/preface-3e.html)  

# Cheat sheets

[rmarkdown cheat sheet](https://www.rstudio.com/wp-content/uploads/2015/02/rmarkdown-cheatsheet.pdf)  
[math in rmarkdown](https://rpruim.github.io/s341/S19/from-class/MathinRmd.html)  
