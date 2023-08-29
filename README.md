# KiCad library #

This repository stores KiCad libraries (symbols, footprints and 3D models).

The version currently being used is [KiCad 7 for Linux](https://www.kicad.org/download/linux/).

## Create a new project ###

### Create KiCad project
* Open KiCad 7.
* Create a new project ```File -> New Project...```
* Write the project name (same as repository name) and select the project directory.
* Open a terminal an go to the project directory ```cd <PROJECT_DIRECTORY>```
* Create a new GIT project ```git init```
### Create git repository
* Create a GitHub repository with the same name as KiCad project (default branch name: ```master```). It is important not to create README and .gitignore files.
* Set the GIT remote ```git remote add origin git@bitbucket.org:<YOUR_BB_USER>/<PROJECT_NAME>.git```
* Create a README and a .gitignore.
* Create a lib directory ```mkdir lib```
* Go to lib directory ```cd lib```
* Add this repository as submodule ```git submodule add git@github.com:GuilleGonzzalez/kicad-lib.git```
### Add symbol library to KiCad project
* Open the schematic file (```<PROJECT_NAME>.kicad_sch```).
* Open Symbol Libraries ```Preferences -> Manage Symbol Libraries...```
* Click on ```Project Specific Libraries``` tab.
* Click on directory button.
* Select symbol library in ```lib/kicad-lib/symbols```
* Click ```OK```
### Add footprint library to KiCad project
* Open the PCB file (```<PROJECT_NAME>.kicad_pcb```).
* Open Footprint Libraries ```Preferences -> Manage Footprint Libraries...```
* Click on ```Project Specific Libraries``` tab.
* Click on directory button.
* Select symbol library in ```lib/kicad-lib/footprints```
* Click ```OK```
### Upload project to GitHub repository
* In the project directory, add all new files ```git add .```
* Commit changes ```git commit -m "Initial commit"```
* Push changes ```git push -u origin master```

## Make a release

Create a directory in <PROJECT_DIRECTORY> for all the output files ```mkdir outputs```.
### Schematic
* Open the schematic file and run ```ERC```.
* Check all passive componets have the correct value.
* Complete the page settings with all the information.
* Generate the schematic PDF in ```File -> Print...``` and save it in ```outputs``` directory as ```schematic.pdf```.
### PCB
* Open the PCB file and run ```DRC```.
* Generate the layout PDF in ```File -> Print...``` and save it in ```outputs``` directory as ```layout.pdf```.
* Generate the STEP file in ```File -> Export -> STEP...``` and save it in ```outputs``` directory as ```3d.step```.
* Generate the Gerber files. Detailed instructions for JLCPCB manufacturer are given in this [link](https://support.jlcpcb.com/article/194-how-to-generate-gerber-and-drill-files-in-kicad-6). Save it in ```outputs/gerbers```.
* (OPTIONAL) Generate the pick and place files and save it in ```outputs```. An example can be found [here](https://www.lioncircuits.com/faq/pcb-assembly/how-to-export-Pick-and-Place-Files-using-KiCad).
    * Click on ```File -> Fabrication Outputs -> Component Placement (.pos)...```.
    * Format: ```csv```.
    * Units: ```mm```.
    * Files: ```Separate files for front, back```.
    * Click on ```Generate Position Files```.
* (OPTIONAL) Generate the BOM files as described in the section ```How do I generate a BOM file?```.
### BOM file
* Check that every component has the following properties: ```Reference```,
```Value```, ```Footprint```, ```Manufacturer```, ```Manufacturer PN```, ```Supplier``` and ```Supplier PN```.
* Open BOM generator ```Tools -> Generate BOM...```.
* Add the BOM generator located in ```bom``` directory of this repository clicking ```+``` button.
* Click on ```Generate```. This will create a ```bom_<PROJECT_NAME>.xlsx``` file in ```<PROJECT_DIRECTORY>/outputs```.
* Open the file and review the result.
* Export it as PDF and save it in ```outputs``` directory.

### Board Stack Report
In this repository there is a folder named ```board_stack_report``` where are templates for make a report of different PCB thickness.

### Git
* Create a tag with the version ```git tag -a <REVISION> -m "<REVISION>"```.
* Push changes to git ```git push origin <REVISION>```, ```git push```.
* Zip all files of the ```outputs``` directory and upload it with this name ```<PROJECT_NAME>_v<REVISION>.zip```. Example: ```my_proj_v1_0.zip```.
