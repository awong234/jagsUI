jagsUI
==========

# Fork info

Markov Chain Monte Carlo iterations are, as the name implies, stochastically dependent upon previous samples drawn from the posterior distribution in a Markov fashion. The `autojags` function allows a check of the diagnostic Rubin-Gelman test at breakpoints specified by the user. However, given that these breakpoints exist, it should be possible to save the state of the MCMC chain to resume at a later time, in the case of power outages, for example. This fork modifies `autojags.R` to provide start/stop functionality and MCMC chain backups for the `autojags()` function. Major differences include:

* Argument `continue` allows user to continue based of MCMC chain backup file, saved as a simple `.Rdata` file in the working directory. Setting `continue == F` is identical to running `autojags()` as normal.
* Argument `savePath` allows user to specify path to save backup file save path.
* Argument `fileTemplate` allows users to specify the name of the output MCMC objects.
* MCMC chain states at every check are saved, no different functionality implemented at this time.

NOTE: While this fork was used successfully in my thesis analysis, I make no guarantee of flawless function. Observed bugs include improper assignment or structure of DIC variable causing error in the print method for `jagsUI` summaries. The calculated DIC is still accessible within the output file, however.

# Continue readme

This package runs JAGS (Just Another Gibbs Sampler) analyses from within R. It acts as a wrapper and alternative interface for the functions in the rjags package and adds some custom output and graphical options. 

There are several other similar packages (R2jags, runjags, and of course rjags itself). I wrote this one to allow tighter control over the JAGS adaptive and burn-in periods (see the issue described here: http://stats.stackexchange.com/questions/45193/r2jags-does-not-remove-the-burn-in-part-sometimes) and to simplify other common tasks such as formatting data, plotting results, and running chains in parallel.

To install the package independent of CRAN:

1. Install the latest version of JAGS on your computer (http://sourceforge.net/projects/mcmc-jags/files/JAGS/). If you have a 64-bit OS, you may need to install both the 32 and 64 bit versions of JAGS (if available). If you are running R 3.3.0 or later on Windows, make sure you install the correct version (see release notes).
2. Download the latest source package .tar.gz or Windows binary .zip file from the 'Release' tab of the repository (https://github.com/kenkellner/jagsUI). 
3. The jagsUI library requires packages rjags and coda. If you have previously installed the coda and/or rjags packages, I highly recommend removing and re-installing them first:

        remove.packages(c('coda','rjags'))
        install.packages(c('coda','rjags'))
4. Finally, in R or Rstudio, choose to install a package from a local/archive file and select the downloaded package.

Alternatively, you can install directly from R, using package devtools (which installs the other required packages automatically). Devtools may complain that Rtools are not installed, but they are not necessary to install this package, so you can safely ignore the warning.
```
remove.packages(c('coda','rjags'))
library(devtools)
install_github("kenkellner/jagsUI")
```
Acknowledgments: Martyn Plummer, developer of the excellent JAGS software package and the rjags R package;  Andrew Gelman, Sibylle Sturtz, Uwe Ligges, Yu-Sung Su, and Masanao Yajima, developers of the R2WinBUGS and R2jags packages on which my work is based; Robert Swihart, Marc Kery, Jerome Guelat, and Michael Schaub, who tested and provided helpful suggestions for early versions of the package.
