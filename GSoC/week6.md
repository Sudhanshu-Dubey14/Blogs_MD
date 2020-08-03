% GSoC Days: Week 6

The week started with me integrating the manager module with the example GUI. So now there was a 'Run' button usling which you can get an example automaticaly solved.
Also last week, Bernd had given me some examples which he had written around a year ago in his [GitLab repo](https://gitlab.com/wartburgritter/fcusermod/-/tree/master/FEMExamples), so I had a look at them and selected 4 examples which were already not here in FreeCAD.

Then I started working on the electrostatic example of Elmer. The model of this example was different then other examples on which I have worked as it was made using the [Sketcher](https://wiki.freecadweb.org/Sketcher_Workbench) workbench and not the [Part](https://wiki.freecadweb.org/Part_Module) workbench. Essentially, I used Sketcher from inside the [PartDesign](https://wiki.freecadweb.org/PartDesign_Workbench) workbench. But this was my first time using Sketcher. What you can do in Sketcher is make a sketch and then apply the required constraints to fit it to your requirements. Then in PartDesign you give your 2D sketch a 3rd dimension by extruding it. And boom, you have a 3D model ready. Though it isn't that easy to programme the model using Sketcher, and it isn't even recommended by Bernd. But then we didn't had any example made in Sketcher and so I went with this difficult option cause learning is fun!

## Backstory of the Example

Coming from the Elmer tutorials, this example has a bit of backstory. The motivation of the case actually comes from [MEMS microphone](http://www.eeherald.com/section/design-guide/mems-microphone.html). These are electronic microphones that are increasingly being used in your phones and laptops.

![MEMS Microphone](https://eeherald.s3.amazonaws.com/uploads/ckeditor/pictures/oldarticleimages/memsmicrophone2.jpg)
![Detailed Diagram](https://eeherald.s3.amazonaws.com/uploads/ckeditor/pictures/oldarticleimages/memsmicrophone3.png)

You see that hole in the back-plate? We are studying a symetric quarter of that hole in this example. And so, everything in our model is just air!!! Yes, even though it might look like a solid model but we have kept it's material as air. So at the end, we are interested in finding the electric force in that environment due to the potential difference.

## Defining Air

So now that we know that our material is air, we need to define it in our example. Yeah for some reason, we don't use the predefined materials in FreeCAD like we do in the GUI. But anyway, I used the values of "Air-Generic" to define my air for the example but when I tried to run it I got error stating that units of `VolumetricThermalExpansionCoefficient` and `ThermalExpansionCoefficient` are wrong. So I had to search the net for them and add the correct value and unit of these quantities for air.
But even after that, Elmer wasn't picking it up and saying that there are no materials defined!

And that's how the week ended, with me unable to correctly define the most common thing around us. Oh you think air is simple, then explain this comic to me:

![](https://imgs.xkcd.com/comics/ground_vs_air.png)

I knew you couldn't, so let's just visit [explain xkcd](https://www.explainxkcd.com/wiki/index.php/2242:_Ground_vs_Air) *cause we all are dumb*.
