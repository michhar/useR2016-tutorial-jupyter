# useR2016-tutorial-jupyter

Resources for useR! 2016 Reproducible Research tutorial @ Stanford

## Convert notebook to slides and send to browser (Cmd line)
On the command line (this will convert to slides and open a brower window to serve them up!):

>  `jupyter nbconvert "How to create a Jupyter presentation.ipynb" --to slides --post serve`

## More conversions of notebooks (Cmd line)

**to pdf (converts to latex first)**

  `jupyter nbconvert "notebookname.ipynb" --to pdf`
  
**to latex (in case to pdf does not work and you need to fiddle)**

  `jupyter nbconvert "notebookname.ipynb" --to latex`
  



