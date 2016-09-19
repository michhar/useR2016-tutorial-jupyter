A few notes:

	1. All of the commands I run in the Command Prompt (use Admin Command Prompt only when specified)
	2. For python module installs I will use "pip" or "pip3" (for python3) python package manager
	3. I use the word terminal and Command Prompt interchangeably

## Pre-Requisites (32-bit recommended)

	1. Python 2.7 (https://www.python.org/downloads/release/python-2710/)
	2. Python 3.4 or 3.5 (https://www.python.org/downloads/windows/)
	3. R (I installed 3.2.2)

A restart is required to use python from the command line (i.e. it adds it to path).

R is not automatically added to the PATH variable.  If you want to call it from the command line you must add it by:

Go to Control Panel -> System and Security -> System -> Advanced system settings -> Environment Variables

On the lower screen you will see "System variables".  Select "Path" and then "Edit".  I added these two entries:

 "C:\Program Files\R\R-3.2.2\bin\"
 "C:\Program Files\R\R-3.2.2\bin\x64\"

(note:  your path to the R executable might be different for a different version)

To check your path in terminal
echo %PATH%

Python Modules Commands
	1. pip3 install jupyter notebook

## Getting R Ready

Open an R GUI (rgui.exe or RStudio) or R command line interpreter and run these  commands (installs R kernel and tells jupyter about it, also installs for user and hence uses a local user R library directory):
		a. install.packages(c('rzmq', 'repr', 'IRkernel', 'IRdisplay'), repos = c('http://irkernel.github.io/', getOption('repos')))
		b. IRkernel::installspec(user = TRUE)

Check that the IRKernel is now an option on jupyter with this command (should be one named 'ir'):

jupyter-kernelspec list

BTW:  if you want additional R packages just install them with:

install.packages(<pkg name>, repos = "http://cran.us.r-project.org")
	
Start the notebook in terminal by:
	• this will open it up in a browser
	• first cd to a working directory of your choosing

jupyter notebook

## Troubleshooting

	1.  Packages not found I.e. "Warning in install.packages : package ‘IRkernel’ is not available (for R version 3.2.3)"
		a. e.g. package jpeg was installed by specifying a different repo: install.packages("jpeg", repos = c("http://www.rforge.net"))
	2. Need some dependencies not covered by an install_github install
		a. e.g. package digest, uuid, evaluate (R will warn if using install.packages, but not if using install_github from devtools)
	3. Update R path
	4. Update lib paths
		a. RStudio R lib paths are different than native R has.  Jupyter uses native R paths.  If installing libraries with RStudio, one should make sure that path is in Rprofile.site or .Rprofile user settings file in home dir.
		b. I put this in an .Rprofile file that lives in my home directory to add a library path (this tells native R to also look into the library RStudio uses which I found out with .libPaths in RStudio):
			i. .libPaths( c( .libPaths(), "C:/Users/michhar/Documents/R/win-library/3.2") )
	5. If you have Python2 only in your notebook and you also want Python3 do this:
		a. (NOTE: I have the vanilla python 2.7 and 3.4 install, i.e. not anaconda or miniconda; python3 is my default python - which I set in my environment variables by placing python34 first in my path)
		b. (NOTE2: if you reset a path, must open a fresh command prompt to use current path settings)
			i. pip3 install ipython ipykernel
			ii. ipython3 kernel install --name python3 --display-name "Python 3"
	6. If you have Python3 only in your notebook and you also want Python2 do this:
		a. pip install ipython ipykernel (NB: Use python27 pip!!)
		b. ipython2 kernel install --name python2 --display-name "Python 2"
If using conda and Ressentials make sure your R version is one belonging to conda

## Alternate approaches

-Docker images (will have to run VM)
  - https://github.com/jupyter/docker-stacks/tree/master/datascience-notebook
  - https://bitbucket.org/rpy2/docker-rpy2-release


If I wanted R kernel system-wide I'd have to put necessary libraries in System R library folder as well as specify user = FALSE when installing kernelspec:
(just note that install.packages() from within notebooks will NOT work because library path is system and notebook will NOT have permission)

Here we do installs from the current working R install (whatever is on PATH).  In my case it's R-3.2.2

In R-3.2.2 (as admin):
From admin command prompt start R:
C:\Program Files\R\R-3.2.2\bin\x64\Rgui.exe

Once in Rgui run these lines:
install.packages(c('rzmq','repr','IRkernel','IRdisplay'), lib='C:/Program Files/R/R-3.2.2/library', repos = c('http://irkernel.github.io/', getOption('repos'))
library(IRdisplay)
IRkernel::installspec(user = FALSE)
(Notes: you may have to install some dependencies…just do this and try installspec again)
