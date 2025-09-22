# A few interesting topics

## Jupyter Notebooks

### What are Jupyter Notebooks?

See: https://jupyter.org/

A Jupyter Notebook is a document that can contain text and Python code. The text is written in markdown (https://www.markdownguide.org/). The code can be executed directl in the document and the output also appears in the notebook.

Notebook can be easily converted to html documents.

These note books are often used in data analysis, scientific research, and education because the can easily combine code, explanation of the code and analysis results in a user-friendly manner. It is a popular tool in the field of data science and machine learning.

Jupyter Notebooks do not only support Python but also R and a few other languages.

### Execute a notebook in Google Colab

The easiest way to execute a notebook is via Google Colab. You surf to https://colab.research.google.com, sign in and you can start. The only thing you need is a Google account.

### How can you execute a notbook locally on your computer?

You can edit and execute notebooks locally as follows:


1. **Installation**:

   - Install Jupyter via pip:

     ```
     pip install jupyter
     ```

1. **Start your server**:
   - Open a terminal or the command prompt.
   - Navigate to the right folder.
   - Type `jupyter notebook` and press Enter.
   - This command will start the Jupyter server and open a web page in your standard browser with an overview of the available notebook and files.
2. **Create a new notebook**:
   - Click 'new' in the Jupyter interface and choose the programming language (usually Python).
3. **Edit**:
   - A notebook consists of cell that contain code of Markdown text.
   - Click in a cel to edit it.
   - To add code to a code cell: just type your code in the cell.
   - For text: change the cell to Markdown mode (in the drop-down menu at the top) en add your text.
4. **Execute**:
   - Execute a cell by clicking on the cell and press 'Run' at the top of use the shortcut key 'Shift-Enter'.
   - The output of your code will appear directly under the cell in question.
   - You can execute several cells one after the other and go through a number of calculations or data analyses step by step.
5. **Save**:
   - Your notebook is automatically saved.
   - You can use the 'Save' button or use the shortcut key 'Ctrl-s' (or Command-s on Mac).
6. **Extra options*
   - You can move, delete or add cells using the toolbar at the top.
   - The are other options such as zooming in and out, searching in your notebook, and so on.
7. **Shut down**:
   - Close the notebook by choosling 'Close and Halt' in the menu.
   - Stop the Jupyter server by pressing 'Ctrl-c' in your terminal.

Next to Jupyter notebook we also have JupyterLab, a more extensive and integrated environment for Jupyter notebooks.

### Execute Jupyter notebook in an IDE.

IDE's such as Jetbrains' Pycharm or Visual Studio Code support executing Jupyter notebooks directly or by installing a plug-in. 



