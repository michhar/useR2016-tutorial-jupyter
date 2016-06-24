# useR2016-tutorial-jupyter

Resources for the UseR!2016 tutorial using Jupyter Notebooks

## Converting notebooks to other formats

You can use the command line (e.g. bash) to convert notebooks to various formats


1. to slides and send to browser

    - this will convert to slides and open a brower window to serve them up!

        ```
        jupyter nbconvert "How to create a Jupyter presentation.ipynb" --to slides --post serve
        ```

2. to pdf

    - This requires that you install LaTEX on your system
  
        ```
        jupyter nbconvert "notebookname.ipynb" --to pdf`
        ```
  
3. to latex

    - Use this in case to pdf does not work and you need to fiddle with the LaTEX (yuck)

        ```
        jupyter nbconvert "notebookname.ipynb" --to latex`
        ```
  



