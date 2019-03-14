**How To Do**
=============


**Step 1**
.. code:: bash

        git clone https://github.com/NorwegianVeterinaryInstitute/ORION_HandBook.git

**Step 2**
File index.rst is main file
If you want add new page:

create the new file "new-file.rst" inside docs/source/

Add "new-file" under ".. toctree::" in docs/source/index.rst

.. code:: bash   
       
       about
       howtodo
       new-file
   
**Step 3**
Commit the changes to GitHub

.. code:: bash
    
    git add -A
    git commit -m "Why why why"
    git push


**Step 4**
Rebuild the "redthedocs"

1. Go to "https://readthedocs.org/"
2. Create login - Once you have created you dont need to create everytime.
3. Connect the GitHub ORION_HandBook repository - Once you have connected you dont need to do everytime
4. BUILD - You should rebuild every time you make changes in GitHub
5. Refresh "https://orion-ngs-handbook.readthedocs.io/en/latest/index.html"
