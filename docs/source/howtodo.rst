
Step 1
================
.. code:: bash

        git clone https://github.com/NorwegianVeterinaryInstitute/ORION_HandBook.git

Step 2
================
File index.rst is main file
If you want add new page:

create the new file new-file.rst inside docs/source/ 
Add "new-file" under ".. toctree::"

.. code:: bash   
       
       about
       howtodo
       new-file
   
Step 3
================

Commit the changes to GitHub

.. code:: bash
    
    git add -A
    git commit -m "Why why why"
    git push


Step 4
================

Rebuild the "redthedocs"

1. Go to "https://readthedocs.org/"
2. Create login
3. Connect the GitHub ORION_HandBook repository
4. BUILD
5. Refresh "https://orion-ngs-handbook.readthedocs.io/en/latest/index.html"