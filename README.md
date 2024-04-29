## 3D model Datasets
The 3D model datasets can be found here (3D Dataset was partitioned into two due to GitHub size limits):
- Male Dataset: https://github.com/research-digitized-rhinoplasty/3D-face-morph-dataset-male
- Female Dataset: https://github.com/research-digitized-rhinoplasty/3D-face-morph-dataset-female


# 3D Model Morphing and Generation Software
This software can be used to morph 3D models (.obj format) and create new morphed 3D models in bulk. We use the software to morph 3D models of facial scans however it should work on any 3D models.

To make this software work, Blender Software needs to be installed first. The latest stable version is recommended. This has been tested using Blender version 3.0. 

## Running Instructions
Download the code from this GitHub and then go to the directory where you keep the code. The canvas.blend file, Morphed3DGenerator.py file, and your 3D models to morph should be in the same directory. 
- The canvas.blend is a blank blender file. To prepare this, simply open blender, delete the default cube, light source, and camera (and anything else present) and save the .blend file. This will serve as our blank canvas. This file is provided on this page for your convenience. 
- The Morphed3DGenerator.py is phyton code that accomplishes the morphing.

### Windows Instructions (using the command line on Windows)

```
"C:\Users\path\to\blender\blender.lnk" "C:\Users\path\to\canvas.blend" --background --python "C:\Users\path\to\Morphed3DGenerator.py" 
```

### Mac Instructions (using the Terminal app on Mac)

```
/Applications/Blender.app/Contents/MacOS/Blender canvas.blend --background --python Morphed3DGenerator.py
```

When the above command is executed, the program will prompt you to enter the name of the configuration JSON file as follows: "Please enter the path to the JSON file:" Then enter the name of the JSON file that has the modifications desired. 

You can use the 'CreateMorphingConfigurations.html' file to prepare the JSON file that includes the modifications. A sample JSON file is given (Facial-Deformities.json). See the instructions about how to create a configuration JSON file.

Note:
Due to the huge number of outputs and size of the individual outputs that would be created, you may have to cancel the execution at some point with CTRL+C. If you do this while a file is being exported, it can lead to an incomplete file. Such a file can be disregarded and discarded.

## How to Create a Configuration JSON file

The CreateMorphingConfigurations.html page is used to generate the instructions JSON file. The configuration JSON file is given to the Python script to generate modified 3D models. An example JSON file is provided with the name Facial-Deformities.json. Below is a screenshot of the CreateMorphingConfigurations.html page:


![MicrosoftTeams-image (1)](https://user-images.githubusercontent.com/91271377/190245090-75241145-1a97-4ae1-a609-eb7168d77769.png)


The user needs to enter the names of the model (.obj) file in the ‘Model Name’ textbox. The names of the model (.obj) file and the .json file that contains landmark locations should match and be in the same directory. For example, Sarah.obj and Sarah.json. In this case, you would input “Sarah” as the model name. 

The falloff type specifies how the area around the landmark you are manipulating will be affected by your modification. The options for the falloff type are smooth, sphere, and inverse square. 

The transformation type determines how you manipulate the point. The options are translation and scale. The translation is a shift in 3D space (means addition), while the scale is a multiplier (a value of 1 means no change in scale) that is applied to the distance between the landmark and the origin on a given axis. 

The influence radius represents how far the manipulation will be effective around the landmark.

The landmark abbreviation represents the landmark you want to manipulate. You must have the location of the landmark included in the model’s corresponding json file. For example, if the user enters ‘prn’ into the landmark abbreviation textbox, there must be ‘prn’ (pronasale) listed in the json file and it should have values for "xVal", "yVal", and "zVal" tags in the json file. The xVal, yVal, ZVal values of a landmark specify the current location of the landmark. 

If the landmark is a dual landmark (has a left or right corresponding landmark), then select ‘Yes’ for ‘Is dual landmark’ and then enter dual landmark’s abbreviation. An example of a dual landmark is alar crease - left (ac_l) and its corresponding landmark is alar crease - right (ac_r). Examples of landmarks that are not dual are pronasale/tip (prn), glabella (g), nasion/radix (r).
Users can enter the number of modifications desired for the landmark into the textbox ‘The number of iterations for the landmark.’ Each of the modifications will result in a new morphed 3d model.

Starting Point Adjustment X, Y and Z determines what will be added to the initial location of the landmark’s X, Y, and Z location. The adjustment values can be negative. For example, if the xVal is 75 in the JSON file and starting point adjustment for X is -10, then -10 will be added to 75 to make the starting point of the X value 65.

The values entered into the ‘Magnitude of changes at each iteration’ textbox are added to the previous iteration's location. For example, if the xVal for prn in the JSON file is 75, the number of iterations is 3, starting point adjustment for X is -10, and the magnitude of changes at each iteration is 10. Then three new 3D models will be created with X values 65, 75, and 85. 

Having a negative value for a starting point might be useful if your original 3D model has the x, y, z locations of a 3D model that represents the average measurements. The starting point of the values can be used to move the measurements toward the boundaries of the normal distribution by using -3 times the standard deviation as its starting point, having the magnitude of changes as the standard deviation and number of modifications as seven.

After the user enters the above values for a landmark, he/she can click the 'Add Modification' button. This will add the modifications for the landmark into a table. Once the user enters values for all the landmarks he/she wants to modify, he/she can click on the ‘Make and Download the Configuration File’ button to download. The configuration JSON file can then be used as an input for the 3D morphing Phyton code.

The webpage to create a configuration JSON file can be found here: https://research-digitized-rhinoplasty.github.io/3D-face-morph/


This study has been published in Facial Plastic Surgery & Aesthetic Medicine, please use the following to cite:

- Topsakal, O., Glinton, J., Akbas, M. I., & Celikoyar, M. M. (2024). Open-Source 3D Morphing Software for Facial Plastic Surgery and Facial Landmark Detection Research and Open Access Face Data Set Based on Deep Learning (Artificial Intelligence) Generated Synthetic 3D Models. Facial Plastic Surgery & Aesthetic Medicine, 26(2), 152–159. [doi:10.1089/fpsam.2023.0030] (https://doi.org/10.1089/fpsam.2023.0030)
