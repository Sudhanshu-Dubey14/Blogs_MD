% GSoC Days: Week 2

So after having a basic GUI to list all the examples, we had to catergories them based on their properties. The properties of a FEM example include:

1. Constraints: The type of [constraints](https://wiki.freecadweb.org/FEM_Module#Electrostatic_Constraints) being used in the example.
1. Equations: What is the type of equation (mechanical, thermal, electrostatic, etc) being solved in the example.
1. Materials: The type of [material](https://wiki.freecadweb.org/FEM_Module#Materials) the model in the example is made of.
1. Mesh: What is the shape of the [elements](https://wiki.freecadweb.org/FEM_Mesh#Mesh_elements_in_FreeCAD) of the [mesh](https://wiki.freecadweb.org/FEM_Mesh).
1. Solvers: Which [solvers](https://wiki.freecadweb.org/FEM_Solver) present in FEM workbench can solve the example.

For getting these information from the examples, we decided to add a convinience method `get_information()` which would return us a dictionary containing all the information of the example.
But there was a catch here! To use this method, I would need to import the example modules. And while this can be as simple as `from example import get_information` we can't do that. Why? Cause the list of examples is meant to grow so it has to be dynamic. Also, the simple way would require us to think of unique names for the `get_information` of each example which is a tedious task. 
So I searched and found that we can dynamically import modules using `importlib` package. Further we can use `getattr()` method to get the method from a module and execute it. Thus, we built a GUI that dynamically loads all the examples that have a `get_information` method, classifies and displays them. This removes the need to register any new example and also simplifies the testing of an example during it's making. It was quite a satisfaction to make this GUI.

Besides that, nothing much happened. I finally got the rebase right. And the hinged beam example I mentioned earlier was completed (yet to be tested).
Major learnings would be `QTreeWidgetItem`, `importlib` and `patience` :).

And with no relation to this post, here is a nice xkcd:

![](https://imgs.xkcd.com/comics/metamaterials.png)

By the way, how many of you knew that there is a site only to [explain xkcds](https://www.explainxkcd.com/wiki/index.php/1351:_Metamaterials)!!!
