# ME700-ASSIGNMENT3

## Set Up 

Set up the conda environment and test that the code is functioning. Note: The environemnt name for all parts of Assignemnt 1 refers to the bisection method.  

1. Create a new conda environment and activate it.  
    ```bash 
    conda create --name finite-element-analysis-env python=3.12
    ```
    ```bash
    conda activate finite-element-analysis-env
    ``` 
2. Confirm that the right version of Python and pip setuptools are being used. Python should be version 3.12; the second command will update setuptools if necessary.  
    ```bash
    python --version
    ```
    ```bash
    pip install --upgrade pip setuptools wheel
    ```
3. Make sure you are in the ME700-Assignment3 directory.  
4. Install an editable version of the code. Note that the *pyproject.toml* file is required for this.  
    ```bash
    pip install -e .
    ```
5. Install the finite element analysis package from git.
    ```bash
    pip install git+https://github.com/Lejeune-Lab-Graduate-Course-Materials/finite-element-analysis
    ```

## Overview of FEA Code

### Outline of *full_code_example_1.py*
1. Define element type, number of degrees of freedom, domain size (for rectangle), number of elements, and prescribed stretch (lambda).  
2. Call *pre_process.py* to generate rectangular mesh.  
    a.  *pre_process.py* also has code to generate a 2D mesh from an outline; not sure if the rest of the code works with a nonrectangular grid.  
4. Call *pre_process.py* to find the boundary nodes and faces.  
5. Call *pre_process.py* to assign the boundary conditions.  
    a.  The example doesn't have applied loads at the boundary, but these can also be defined.  
6. Define material properties and the number of steps to solve over.
7. Call *solver.py* to solve for node displacements.
8. Plot results with *visualize.py*.

Note: Plotting info in *pre_process_demo_functions.py* is not included in this outline.

### Outline of *solver.py*

__for__ number of iterations  
|    Find load factor = iteration number / number of iterations
|    __while__ error < tolerance  
|    |    Find global stiffness matrix with *assemble_global.py*  
|    |    |    Find local element stiffness for each element using *local_element.py*  
|    |    |    Aasemble global stiffnesss matrix.  
|    |    Find global traction matrix with *assemble_global.py*  (calls *local_element.py*).  
|    |    Find R = loadfactor*F - global residual *******************
|    |    Assign boundary displacements (e.g. fixed nodes don't move).  
|    |    Solve for displacement \delta = K-1R  
|    |    Add displacement to total node displacement.  
|    |    Find error.  
|    Add node displacement to frame displacement list


            



