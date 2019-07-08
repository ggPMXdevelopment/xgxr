# xgxr

The xgxr package supports a structured approach for exploring PKPD data ([outlined here](http://opensource.nibr.com/xgx)).  It also contains helper functions for enabling the modeler to follow best R practices (by appending the program name, figure name location, and draft status to each plot).  In addition, it enables the modeler to follow best graphical practices (by providing an xgx theme that reduces chart ink, and by providing time-scale, log-scale, and reverse-log-transform-scale functions for more readable axes).  Finally, it provides some data checking and summarizing functions for rapidly exploring a PKPD dataset.

## How to update/test/use package
* **Developing the package:** Run [_Package_Setup.R](_Package_Setup.R).  This will update the documentation, reinstall the package, and rebuild the vignette.
* **Installing the package for use in your project:** follow the directions below, also [here](_Package_Install_New_User.R).  There are a few options.
  * **Option 1:** Install directly from Github to a local repository with the following command: `devtools::install_github("Novartis/xgxr", args = c('--library="./"'))`
  * **Option 2:** Download the package as a zip file and build and install it yourself, following the directions below.
    * Download this package as a zip file
    * Place the zip file in your project folder, with your R code. (if you don't have a project folder... create one)
    * Unzip the file.  
    * Open R 
    * Set the working directory to your project folder.
    * Type: `devtools::build("xgxr-master")` (if you don't have devtools, install that first using command: `install.packages("devtools")`)
    * Then type: `install.packages("xgxr-master", repos = NULL, lib = "./", type = "source")`
    * To load the package, type: `library(xgxr, lib.loc = "./")`
  * **Option 3:** Source the R files and read in the data files directly
    * Download this package as a zip file
    * Place the zip file in your project folder, with your R code. (if you don't have a project folder... create one)
    * Unzip the file.  
    * Open R
    * Execute the following code:
      ``` 
      Rfiles = list.files(path = "xgxr-master/R/", full.names = TRUE)
      for(ifile in Rfiles) {
        source(ifile)
      }
      
      Rdafiles = list.files(path = "xgxr-master/data", full.names = TRUE)
      for(ifile in Rdafiles) {
        load(ifile)
      }
      ```
  * **Last Resort Failsafe:** If you want to make use of the xGx exploratory graphics principles but are unable to install the package `xgxr`, you can view an older version of the website that does not make use of the `xgxr` package.  http://opensource.nibr.com/xgx_v1
  

## Overview for how R packages (including this one) are organized
* Functions are located in the "R" folder.  
  * When creating a new function, copy an existing one and follow the same format, with the documentation in the header
  * When creating a new function, make sure to also add example code and some code to the vignette.
  * For the function to be visible after the package is loaded, make sure to have the @export line.  
* Sample datasets are stored in the inst/extdata folder as "external datasets" as csv files
  * They can be loaded like any other CSV file.  To get the filename, type for instance: filename   = system.file("extdata", "Multiple_Ascending_Dose_Missing_Duplicates.csv", package = "xgx", mustWork = TRUE)
  * We prefer this over the Rda format so that any user can quickly browse the data, even without R.
  * Code for generating these datasets is stored in the data_create folder
* Documentation is located in the "man" folder.  Do not edit this folder.  Instead, edit the documentation within the function header.  
  * Further details on this process are located [here] (https://cran.r-project.org/web/packages/roxygen2/vignettes/roxygen2.html).
* Vignettes are documents that show how a package can be used.  They are located in the "vignettes" folder.  Build them using the devtools::build_vignettes() function.
* The DESCRPTION file is where you list the dependencies on any other packages.
* The NAMESPACE file lists which packages are exported.  It's automatically generated by the devtools::document() command

## Your contribution
* If you will be helping to contribute, we make an effort to follow the [tidyverse style guide](https://style.tidyverse.org/index.html).  Though the one exception is that some of us like equals signs.

## Here are some links for learning more about packages
* [Hilary Parker's brief intro](https://hilaryparker.com/2014/04/29/writing-an-r-package-from-scratch/)
* [Hadley Wickham's book](http://r-pkgs.had.co.nz/)
* [Developing package with Rstudio](https://support.rstudio.com/hc/en-us/articles/200486488-Developing-Packages-with-RStudio)
* [Getting a package onto CRAN](https://cran.r-project.org/web/packages/policies.html)

## Scope of the project
* Base case (100%)
    * Helper functions - log scale, etc… ci [DONE]
    * Vignettes that show idea and work with examples in nlmixr/ggpmx [pk-DONE, pd-TO DO]
* Upside (80%)
    * Overview Plots: xgx_explore_pk(data,units), xgx_explore_pd, xgx_explore_pkpd [pk-IN PROGRESS, pd-TO DO]
      * (continuous, binary, RO)
      * repeated time to event
    * xgx_check_data() - [DONE]
* Stretch goal (40%)
    * RECIST, liver enzymes, etc

## Roadmap
* Continue coding
    * Finish base case at minimum, and possibly the upside
    * Base case and Upside tasks are marked as high or medium priority under Issues.
    * Continue informal discussions with people
* Continue to get feedback from others
    * R subject matter experts
    * nlmixr/ggpmx trainers
    * training courses
* Begin process of "validation" for CRAN and for internal systems
    * make use of Rtemplate from Sebastian Weber
    * implement some testing
* Put version 1 onto CRAN and internal systems

## Steps for getting an R package into CRAN

From [here](https://kbroman.org/pkg_primer/pages/cran.html)
* From Rstudio, run `devtools::check()`
    * Alternatively one could navigate to directory containing package and type: `R CMD build ./`  
    * This will create a .tar.gz file (e.g. `xgx_0.0.1.005.tar.gz`)
    * Then, type: `R CMD check xgx_0.0.1.005.tar.gz --as-cran`
    * The devtools::check() above does the same thing (I think)
