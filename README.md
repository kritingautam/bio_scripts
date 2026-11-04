The trial-and-error cheat code:
Always try installing with bin/pip first since it's faster and handles 90% of standard packages. 
If your terminal explodes into a massive wall of red text complaining about missing gcc, 
clang, or header files (.h), that is your definitive sign to switch over to conda install -c conda-forge.
------------------------------------------------------------------------------------------------------------------------
for example: 
this one first: /opt/anaconda3/envs/stable_opencadd/bin/pip install redo
then try this: conda install -c conda-forge openbabel -y
then get help......

------------------------------------

1. Terminal & Directory Navigation Basics
Commands inside the terminal are case-sensitive, space-separated, and require exact paths.
Action	Command	Example
Where am I?	pwd	Displays /Users/username/project
List folder contents	ls -la	Shows all hidden files, folders, and permissions
List with file types	ls -F	Adds suffixes: / for folders, * for executables
Open folder in Finder	open .	Instantly opens your current directory in macOS Finder
Change directory	cd <path>	cd /opt/anaconda3/envs
Move up one directory	cd ..	Moves from stable_opencadd up to envs
Home directory shortcut	cd ~	Jumps directly to your home folder


2. Environment Architecture (bin vs python vs pip)
Your environment (stable_opencadd) is a structured set of folders on your computer:
The Shed (bin/ directory): A folder holding executable program files (e.g., python, pip, jupyter).
The Engine (bin/python): The actual Python executable file sitting inside bin. When you select your Jupyter kernel, it points directly to this file.
The Delivery Runner (bin/pip): The installer executable sitting inside bin. It fetches packages from PyPI and drops them into your library storage.
The Warehouse (lib/python3.10/site-packages): The internal folder where Python stores installed packages (nglview, pandas, opencadd) so import statements can find them.
Path Syntax Rule: /opt/anaconda3/envs/stable_opencadd/bin/pip names the pip program file inside the bin directory. Adding an extra slash (bin/python/pip) fails with not a directory because python is an executable file, not a folder.

3. Package Management Decision Tree (conda vs pip)
Manager	Target Use Case	Example Packages	Primary Source
conda	Compiled C/C++ libraries, non-Python system binaries, macOS ARM64 structural dependencies	openbabel, rdkit	-c conda-forge
pip	Pure Python utilities, standard ecosystem packages, Jupyter widgets	redo, nglview, pandas


BIOINFORMATICS DEPENDENCY WORKFLOW:

1. Create a clean Python 3.10 environment:
   conda create -n stable_opencadd python=3.10 -y

2. Register the notebook kernel:
   /opt/anaconda3/envs/stable_opencadd/bin/python -m ipykernel install --user --name stable_opencadd --display-name "Python (stable_opencadd)"

3. Try installing standard Python packages via direct pip path first:
   /opt/anaconda3/envs/stable_opencadd/bin/pip install redo nglview ipywidgets

4. If terminal crashes with missing C/C++ compilers, headers (.h), or clang errors, 
   install system binaries via conda-forge before running pip:
   conda install -c conda-forge openbabel -y (see note at the top)
