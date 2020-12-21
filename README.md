### convention
 #### isset vs empty
   - isset()
     - return TRUE if a variable has a value ,  
       ```diff 
       + including (False, 0 or empty string)
       - not NULL
       ```
     - FALSE otherwise
   - empty()
     - return TRUE if a variable has 
       ```diff 
       + empty value, empty string, 0, NULL or False
       ```
     - FALSE otherwise
 
