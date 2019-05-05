# Getting to know the ````__init__.py```` File

So in our [last discussion](https://hacksd.wordpress.com/2019/04/13/steps-to-include-a-new-solver-in-freecad/) we talked about the steps that should be taken to include a new solver in FreeCAD.
If you remember, a part of the first step was to create \_\_init\_\_.py file.
Now what is this file? And what does it do?
Today we will seek answers to these questions.

### What is ````__init__.py```` file?

From [python documentation](https://docs.python.org/3/tutorial/modules.html#packages) "The ````__init__.py```` files are required to make Python treat directories containing the file as packages." 
In simpler words, if you want to import your directories as python packages and the files in them as python modules, then you need to have an ````__init__.py```` in that directory.
It kind of works like specifying ````package <package_name>```` inside a java file which is within a directory called package_name. Only that, this seems like a simpler and cleaner approach compared to the java one.
In the OOPS terms, I would describe ````__init__.py```` as the "constructor" of the package. Why? We will see.

### What to put in ````__init__.py```` file?

In the easiest way, this file can be kept empty. 
I am going to keep it empty too since I have nothing in particular to put here. My only purpose for creating this file is to make python treat my directory as a package since the files (modules) in it need to be imported elsewhere.

But there is much more that you can do with the ````__init__.py```` file.
A quick about this file that I found is [this one](https://pcarleton.com/2016/09/06/python-init/).
