


# Unreal 3D Bounding Box Plugin

Welcome to the documentation of the Unreal 3D Bounding Box Plugin. A plugin designed to generate synthetic Image Detection datasets by exporting the 3D bounding boxes of meshes in an Unreal scene.

## Labeling Actors
For each element in your scene you wish to track, add two ***actor tags*** to your element's actor: the first tag is your label (e.g., "car"), and the second tag must be "3D". 
The first tag will be used in the label file. The second tag is just here to tell the plugin to track the actor.

![actor tags](https://github.com/Plasma-Lab/Unreal-3D-Bounding-Box-Plugin/blob/main/images/tags.PNG?raw=true)

## Setup the camera

The plugin uses a custom camera to be able to extract the 3D bounding boxes.
The camera is in the "content" folder of the plugin with the name **BP_3DBB_Camera**.  Drop the camera in the scene and point it in direction of the tracked objects.
You can see what the camera sees by opening the file next to it called **RT_Capture**.

![files](https://github.com/Plasma-Lab/Unreal-3D-Bounding-Box-Plugin/blob/main/images/files.PNG?raw=true)

![camera](https://github.com/Plasma-Lab/Unreal-3D-Bounding-Box-Plugin/blob/main/images/camera.PNG?raw=true)

## Setup bounding box tracking

By default, the plugin will take 1920x1080 screenshots but you can choose a different resolution and FOV in the details pannel in the  **BP_3DBB_Camera**.

![camera settings](https://github.com/Plasma-Lab/Unreal-3D-Bounding-Box-Plugin/blob/main/images/camera_settings.PNG?raw=true)


## Take captures

Now to take screen captures with bounding box label file, just use the **Take Screenshot With 3D Bounding Box** blueprint.
You can either bind this blueprint to a keyboard key and tie the camera to your player view or program camera movements and automaticaly fire screenshots. (The plugin doesn't support this, you have to set this up yourself.) 

![screenshot](https://github.com/Plasma-Lab/Unreal-3D-Bounding-Box-Plugin/blob/main/images/blueprint.PNG?raw=true)

Just set a path to save the captures, press Play and fire the blueprint!
You also have the option to: 
-  limit the distance from the camera where boundinx boxes will not be detected anymore (in cm, default: 3000 (30m))

It will create 3 folders when taking the captures:

- images: contains the capture files as .png
- labels: contains the label files as .csv
- calib: contains the intrinsics matrix, necessary to project the bounding boxes to screen

# What's in the label file?
![csv](https://github.com/Plasma-Lab/Unreal-3D-Bounding-Box-Plugin/blob/main/images/label_file.PNG?raw=true)

The label file contains 13 columns:


1.  Label: Describes the type of object: 'Car', 'Van', 'Truck' ...
2.  Truncated: Integer (0,1), where truncated refers to the object leaving image boundaries
3.  Occluded: Integer (0,1,2) indicating occlusion state:
	- 0 = fully visible
	- 1 = partly occluded
	- 2 = largely occluded
5. Location: 3D object location x,y,z in camera coordinates (in meters)
6. Dimensions: 3D object dimensions: height, width, length (in meters)
7. Rotation: 3D object rotation in quaternions: qx, qy, qz, qw



You can use the python notebook to visualize the 3D boxes: get the [notebook here](https://github.com/Plasma-Lab/Unreal-3D-Bounding-Box-Plugin/blob/main/3D_Bounding_box_projection.ipynb). (only for the CSV format)

![results](https://github.com/Plasma-Lab/Unreal-3D-Bounding-Box-Plugin/blob/main/images/result.png?raw=true)
