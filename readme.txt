////////////////
///HOW TO USE///
////////////////

You can test the project either :
- in the editor by launching the .uproject
- generating the VS project files and compiling the .sln
- launching the .exe in the Build/Windows folder

In the editor, just play the current level and you will see the result

In the game you can move with WASD or the arrows and the camera with mouse click and moving the mouse

You can use the UI to change the dimension of the maze (between 1 and 255 and should be at least two rooms)
You can check if you want the instant build or over time
The reset maze button will erase the current maze and start a new build

The rooms are marked S / T / E for Start, Treasure, Exit

You can modify the parameters directly in the editor if needed :


BP_Maze :

	Category "Maze" :
		- Room scale value (the scale of the room)
		- Room unit size (the unitary size of a scale one depending on the object used, don't touch if we keep the base wall)
		- Build over time 

	MazeAlgorithmComponent :
		Category "Algorithm" :
			-Width and Height for the number of rooms 

//////////////////
///ARCHITECTURE///
//////////////////

The AGDMMaze is responsible for drawing the maze and contains a component UGDMAlgorithmComponent responsible for the logic of the algorithm to build the maze.

Algorithm :
1. We are building the outside walls of the maze
2. Wall placing loop :
	a. Random a wall position in the maze 
	b. Check the neighbours walls to see how many ends of our current wall is in contact with a neighbour wall
	c. If only one end is connected then we can build it, otherwise repeat the loop until we reach the maximum number of tries (Width * Height)
3. Random the rooms positions

//////////////////
////CONCLUSION////
//////////////////

Pros:
- Easy to implement
- Fast processing
- always a solution

Cons:
- only squared rooms
- only orthogonal walls

//////////////////
////WHAT NEXT/////
//////////////////

1.
Use the same algorithm to generate the walls but consider them also as rooms :
- You can then use diagonal wall so the path will not always be orthogonal
- The tests for the neighbours would be bigger and hard to optimize because we would need to know all the matching wall combination

2.
Use a completely different algorithm using the Delaunay triangulation to generate random rooms of different size, shape and position.
- Generate rooms
- Separate them
- Chose random ones base on a criteria (like size)
- Use Delaunay triangulation to build a graph connecting these rooms
- Build a spanning tree from this graph and build the connections between the rooms


