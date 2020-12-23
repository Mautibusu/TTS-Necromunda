# TTS-Necromunda: raw files
This section is intended to store the intermediary files needed to create models.

It also contains material and information about creating your own models, and importing them in TTS, to explain how to contribute to this repository.



## Workflow Overview to contribute to this repo
You can commit your changes back to the repository at any stage, from github desktop. It is good practice to add some infos about what you have done for each commit.

First, you need to create a model, using photogrammetry:
- take good pictures
  - model reconstruction from images using Zephyr
  - model cleanup and scaling using Blender
  - import into TTS and final check

Then, you need to properly add the assets to this repo:
- choose a unique, descriptive name for your file (counter-example: "Goliaths_1")
- add description to README, following existing format
- create a subfolder in "raw/{FILE_NAME}/" for your project. (example: "raw/Goliaths_1")
- optional: add raw and intermediary files in subfolder "raw/{FILE_NAME}/"
	- raw pictures in subfolder "pics"
	- Zephyr masks in subfolder "pics"
	- Zephyr project, intermediary and output files in subfolder "zephyr" => nope, this file is too big for some reason.
	- Blender project and output files in subfolder "blender"
	
- place your final .obj and .jpg (3D model and texture) in the "raw" folder. Push them to github, and get the full URL for them
- import assets into TTS, using the github URL for mesh and texture.
- save object and place resulting .png and .json files (thumbnail and asset description) in the "models" folder.
- Push final model/asset description to github: .json and .png

## Creating a Model with Photogrammetry - Detailed Workflow
{what's the starting point, what's the end result. What you need. How much effort it takes.}

### Taking pictures
Ensure a good input otherwise the reconstruction will fail or be poor. You can get proper results with a smartphone camera.
- choose a good background. You can build a super simple photobooth with white paper. White works well, unless you model has ton of white: select matte black.
- take about 20 pictures at eye level, 20 from slightly above, then 10 from above.
- make sure to have:
  - proper lighting of your mini
  - good focus
  - no part of the mini out of frame, but also mini occupies about 50% of the images
  - no moving background/other elements
  - no reflexions/shadows

### Image processing with Zephyr
There are other software to do this, but Zephyr works beautifully. You can use the free or lite version. Free is limited to 50 images, but that's usually enough.

Note that from one run to another, Zephyr keeps your settings, so you don't have to review them too closely each time.
Of course, you should also do your own experiments, and the parameters hereafter are just some that have worked for us.

There are several processing steps once you have imported your images:
- masking, where you tell the software where to focus its analysis
- point cloud generation, where the software does a first level of image matching and reconstruction
- point cloud cleaning, where you remove some points that are artefacts
- mesh and textured mesh generation, where you generate the final shape and texture
- export of 3D object and texture, where you get the end result ready to be further processed.

#### Masking
For each picture, you want to tell the software what is the object to reconstruct, and what is background. There are several ways to achieve that.
If your background is perfect, you can select it by color. But it is not so great with DIY smartphone taken pictures...

<a href="url"><img src="doc-scrnsht_masking1.png" align="center" width="600" ></a>
<a href="url"><img src="doc-scrnsht_masking2.png" align="center" width="600" ></a>
<a href="url"><img src="doc-scrnsht_masking3.png" align="center" width="600" ></a>
You can also give examples to the software of what is background and what is object to reconstruct, with red dots (object) and blue dots (background).
This method is what works best. Use a small brush, place blue dots on all areas of background, and a red dot on the miniature.
The software will compute the mask: a red highlight over all of the miniature. Check that no background is highlighted, and no miniature isn't.
You can correct this with the lasso tool (and +/- to add or remove from the mask)

Make sure you have a mask for every picture.
#### Point clouds
Import all 50 images and masks, then check the camera settings (should be done automatically).


Creating the pointcloud is done in two steps: sparse, and dense point clouds.

Select Advanced, then for the sparse point cloud parameters:

<a href="url"><img src="/doc/doc-scrnsht_sparse-params1.png" align="center" width="600" ></a>

Then hit run. It will take a while... but masking reduces the amount of data your computer has to process.

Once finished, make sure that the reconstruction is successful, and that all cameras have a 'YES'.
If that is not the case, you need to review your masking and/or picture taking process.

You can also have a look around at the sparse point cloud, if something looks weird or not covered at this stage, later stages will not work.


Select Workflow->Advanced->Dense point cloud generation, and use these parameters :
<a href="url"><img src="/doc/doc-scrnsht_dense-params1.png" align="center" width="600" ></a>

Hit "Run", it will also take a while.

Once finished, check the resulting point cloud. If anything looks wrong, go back and redo previous steps.

The next step is cleaning of the point cloud and removing noise, eg points that should not be used when reconstructing the mesh.
First, you should clone the Dense point cloud, in case you clean "too much" and need to get back.

Then, here are the steps to select and then delete bad points:
- plane to remove under base/around base
- view from all angles, and lasso.
- selection by color: pick bright white, then adjust threshold.


#### Meshes
In this step, the point clouds are processed to generate a 3D model and a texture.
Go to Workflow->Advanced->Mesh Extraction

Make sure to select the Dense point cloud that you just cleaned.

Mesh parameters (select Advanced) :
{screenshot?}
- Number of nearest Cameras: 3
- Resolution: 50%
- Noise filtering: 20%
- Speed up level: low
- Hyperplane Matching: On
- Cameras preselection: Off
- Update colors: On

Hit next, then parameters (select advanced) :
<a href="url"><img src="/doc/doc-scrnsht_mesh-params1.png" align="center" width="600" ></a>

Hit "Run", it will also take a while (15mn).

Once finished, check if it worked. If not, go back to your original dense point cloud, and do less cleaning.

At that point, you also want to clean-up the mesh. Again, select "clone and apply" in case something goes wrong you can try again with different parameters. The steps are:
- retopology, to uniformize the vertices (factor 2, 5 iterations, and update the colors)
- decimate, to reduce the number of vertices to 25.000 or less (max number that TTS will import)

Then finally, you can generate the textured mesh. Use these parameters:
<a href="url"><img src="/doc/doc-scrnsht_textured-mesh-params1.png" align="center" width="600" ></a>

- max texture size 2k
img resolution 100%
max vertices 25000
sharpening 25%
default color balance.


#### Export
Export textured mesh: select wavefront obj/mtl, and export as single texture.

- have done the process a few times, and have a good and reliable
Note that once you:

### Model cleanup with Blender

#### Align

#### Scale

#### Sculpt?

#### Paint?

#### Export

### Model creation in TTS

Import the mesh and texture.
Set things up: collider, type of object, description/name.
Save object locally.
Edit json to fix the file path if needed.
