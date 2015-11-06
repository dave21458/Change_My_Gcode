# Change_My_Gcode
For use with 3D Printing

goto https://github.com/dave21458/Phomium.git to run this code

My Target:
The target of this project is to be able to edit a g-code file used in 3D printers.

My thinking:
I am using Java Script to display and edit the g-code.
First step is to parse a gcode file into a js file into a an array of objects. The objects will contain all the data from each line of gcode. Currently I use PHP to do the parsing and creation of a js file. The file is then loaded into the a browser along with other javascript and html.
The js file contains a model array along with a few other vars that gather information about the model. The model array elemets are each layer of the the gcode model. Each model array element is an object that contains arrays for each segment. Each segment array is an object that contains the x,y,z,e data along with other relavent data for dispalying each segment.

What in the gcode?
In 3D modeling a common export file is .STL that most all 3D modeling software can understand. So if you create a model in some CAD program it can be exported as a STL file.The STL contains a series of triangles in 3d space that represent all surfaces of the 3D model.
In 3D printing the STL file is ran through a Slicer program that the model into layers of XY coordinates for a given Z thickness. The Slicer tries to determine XY coordinates of each layer based on width of a single print line. In theory it XY should be offset from the surface by 1/2 the line width. The XY lines are known as the 'tool path'. 
Each line of the gcode file has a command. these commands are either G commands or M commands. Each followed by a command code and any relavent data required to execute the command. G0 and G1 commands are the most common, in 3D printers these have little if any difference in execution. G0 is suppoosed to represent a non-printing move, while G1 are printing moves. However in 3D printing the extruder movement (E data) determines if it prints or not.
The data in the G0/G1 lines is typically X,Y,Z and E(if printing) absoute coordinates. However it is possible that the data is relative to it current position. This is determined by the last G90/G91 code executed. The codes can also contain F data, this determines the speed at which the printer moves or prints. The F data remains valid for all folowing commands until the next line that contains a F data.
