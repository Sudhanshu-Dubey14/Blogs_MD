%GSoC Days: Review Period

After the application period ends, there is a 1 month period in which the organisations review the applications and select the students. Since I had only 2 days to write the proposal, most of my interaction with Bernd and the FreeCAD community regarding this project happened in the review period.

And to be honest, I was very naive during that time and so were my questions (which you can see [here](https://forum.freecadweb.org/viewtopic.php?f=18&t=44705&start=20)). I would ask anything and everything that would come to my mind. But hey, that's how we learn! And I sure learned a lot!!

## Shifting to Arch

The first thing required was to install FreeCAD. I was using Kali Linux during those days and you need to add the [FreeCAD PPA](https://launchpad.net/~freecad-maintainers/+archive/ubuntu/freecad-stable)(Personal Package Archive) but there was some issue with it. I then tried to compile FreeCAD ([which I have done earlier](https://hacksd.wordpress.com/2018/06/03/cloning-and-compiling-freecad/)) but then Kali had both Python 2 and Python 3 so it was messing up. And then I took quite a courageos decision. I shifted to Arch Linux!!!
I had installed it months ago when my Ubuntu got corrupted but only the command line interface was there so I had to upgrade, install and configure the graphical user interface. It took me 5 days to do everything and compile FreeCAD in my new Arch Linux. But shifting to Arch was a very good decision and I have loved Arch since then!

## The First Example

Now that I had FreeCAD with me, it was time to start creating examples. It was already Apr 11 and the only contribution I had made was improving the wiki page that gives instructions to compile FreeCAD on Arch.
The [first example](https://forum.freecadweb.org/viewtopic.php?f=18&t=19037) given to me was quite simple. You have a hollow cylinder, you apply torque on it's outer surface to make it rotate. Only that, there is no way to apply a torque in FreeCAD. But then, torque is simply rotational force. So you apply a force and then tranform the coordinate system to a cyliderical one, which results in torque. Simple right. 
With more questions and answers I started creating this example. The examples are completely in code, so that they can be run without any GUI (which is called FreeCADCmd). So I devised a simple but effective approach:

1. I get it the FreeCAD file having the example.
1. I replicate it in GUI and record the [macro](https://wiki.freecadweb.org/Macros).
1. Get the essential method calls and fit them into the example convention.

For mesh, Bernd just created a [simple way](https://forum.freecadweb.org/viewtopic.php?f=18&t=44705&start=40#p388738) to export the mesh into a python module which is how we import the mesh into an example.

Things were working slow but good. We had alread [resolved some bugs](https://forum.freecadweb.org/viewtopic.php?f=18&t=44705&start=40#p389398) because of this example. Parallely, I started working on another [transform constraint example](https://forum.freecadweb.org/viewtopic.php?f=18&t=20238#p157643). In this, we have a beam which is hinged on it's two ends and we apply pressure from the bottom/top so that it bends a bit from the centre and the hinges rotate slightly.

## Additional Learning

It was almost the end of April. Bernd suggested that we should create a GUI to open examples. This was indeed required as even I struggled initially to run the examples. The GUI was supposed to be built using Qt but I had never worked on it. Neverthless, it's never a harm to learn something. In fact Bernd did the basic setup of the GUI and I had to add a tree view of the example (using [QtTreeWidget](https://doc.qt.io/qtforpython/PySide2/QtWidgets/QTreeWidget.html)).

But I had to get only that commit in which the GUI was setup. Those who know [git](https://hacksd.wordpress.com/2019/02/28/using-git/) know that mergeing would get us everything. So for picking a particular commit, Bernd suggested me to use [`cherry-pick`](https://www.atlassian.com/git/tutorials/cherry-pick) which is quite a cool git feature.

But then I faced issue with running the newly compiled FEM workbench. A library was missing! Strange! Because I could see that library in it's right location but somehow FreeCAD was not able to find it. After some searching, I found a really cool debugging tool for missing libraries which wsa [lddtree](https://codeyarns.com/2015/12/16/how-to-view-hierarchy-of-shared-library-dependencies-using-lddtree/). So building a tree of all the libraries revealed that one of the packages was not upgraded. And indeed it was an [AUR](https://aur.archlinux.org/) package which means that it's my reponsibility to upgrade it. [TIP for Arch Users: Check for upgrades of your AUR packages right after you upgrade the normal packages].

April was over by the time I started working on the ExampleGUI.

But you know, working on GUI is not easy:
![working on GUI](https://external-preview.redd.it/flqgQ0UEPRR8WLjZPdMnKZxLjKDkQpsFx70IlAitwsE.jpg)
