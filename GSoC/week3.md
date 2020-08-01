% GSoC Days: Week 3

So now that two examples were ready, it was time for some testing. And by testing, I mean [unit testing](http://softwaretestingfundamentals.com/unit-testing/). So I need to only test the working of a single unit, which here is an example.
There is already a [testing framework](https://github.com/FreeCAD/FreeCAD/blob/master/src/Mod/Fem/femtest/test_information.md) for the FEM workbench. For examples, the testing idea is simple. Beside testing that the example can be imported successfully, which means that the model is correctly made, the constraints are correctly applied and the mesh is proper, we create the input file for the solver and compare it with a pre-generated input file. This follows the general idea of testing that the generated outcome (the generated input file here) matches the expected outcome (the pre-generated input file).

So I followed the procedure and created unit tests for the two examples. The tests passed (as there was an 'OK' in the end) but I got this 'error' message:
`A finite mesh without a link to a Shape was given. Happen on pure mesh objects. Some methods might be broken.`

I asked Bernd about this and he said that this should be warning and that it's only important if the mesh is a 1D mesh. But our models are 3D and so are our meshes.
You might also have noticed that the error message is saying that it 'happens on pure mesh objects' and indeed we were creating pure mesh objects because all of the other examples were using pure mesh objects too. Now as far as I know, there are 3 type of mesh objects:

1. Pure mesh: This are native mesh object of FreeCAD and are be used when creating mesh [manually using scripting](https://wiki.freecadweb.org/FEM_Mesh#Scripting).
2. [Gmsh mesh](https://wiki.freecadweb.org/FEM_MeshGmshFromShape): This is the mesh object created by Gmsh software.
3. [Netgen mesh](https://wiki.freecadweb.org/FEM_MeshNetgenFromShape): This is the mesh object created by Netgen software.

The reason we were using pure mesh object in examples because we have the mesh as a python module (as I mentioned earlier), some of which were created manually by Bernd. But since now we had the method to simply export a mesh to a python module, Bernd suggested me to replace the pure mesh object with a Gmsh mesh object. This would remove the error message and it did. Later on, I changed the mesh object to Gmsh mesh object in all the examples.

So with this, I had done the first testing of examples in FEM which in itself was the major learning. But you are not always lucky to pass the unit tests. What do you do then?

![](https://pcweenies.com/wp-content/uploads/2013/09/2013-09-23_pcw.jpg)
