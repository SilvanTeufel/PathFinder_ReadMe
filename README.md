# PathFinder_ReadMe
Documentation for a Unreal Engine Plugin
#  AHUDBase

The code snippet provided is written in C++ and utilizes the Unreal Engine. It appears to be a custom implementation of a Heads-Up Display (HUD) that allows the user to select friendly units by drawing a rectangle with their mouse. The code defines a DrawHUD() function for the AHUDBase class, which is responsible for rendering the HUD.

The DrawHUD() function performs the following steps:

1. Checks if bSelectFriendly is true.
2. Iterates over all friendly units in the FriendlyUnits array and calls DeselectAllUnits() on each one.
3. Empties the SelectedUnits array.
4. Gets the current mouse position and stores it in CurrentPoint.
5. If the difference between the current mouse position and the initial mouse position (InitialPoint) is greater than or equal to 2, the function draws a rectangle using the DrawRect() function.
6. Calculates the center points and coordinates of the selection rectangle.
7. Draws the selection rectangle using the DrawRect() function.
8. Calls the GetActorsInSelectionRectangle() function to get an array of all actors (in this case, friendly units) that are within the selection rectangle.
9. Calls the SelectUnit() function on each actor in the array.


The following is a list of all the methods used in the code snippet, along with a brief description of each method:

DrawHUD(): A function that is called by the engine to draw the HUD.
bSelectFriendly: A boolean variable that is used to determine whether the user is selecting friendly units.
FriendlyUnits: An array of AUnitBase pointers that stores all friendly units.
DeselectAllUnits(): A function that is called on each friendly unit in FriendlyUnits to deselect it.
SelectedUnits: An array of AUnitBase pointers that stores all currently selected units.
GetMousePos2D(): A function that returns the current position of the mouse as a FVector2D object.
InitialPoint: A FVector2D object that stores the position of the mouse when the user first started drawing the selection rectangle.
DrawRect(): A function that is used to draw rectangles on the screen.
LengthLineA and LengthLineB: Float variables that store the lengths of the two lines that make up the selection rectangle.
LineCenterPointA and LineCenterPointB: FVector2D objects that store the center points of the two lines that make up the selection rectangle.
InitialSelectionPoint and CurrentSelectionPoint: FVector2D objects that store the coordinates of the selection rectangle.
GetActorsInSelectionRectangle(): A function that is called to get an array of all actors that are within the selection rectangle.
SelectUnit(): A function that is called on each actor in the GetActorsInSelectionRectangle() array to select it.

#  APathProviderHUD

```cpp
void APathProviderHUD::BeginPlay()
```
This is a method that overrides the BeginPlay method of the AActor class. It is called when the actor is first spawned into the game world. In this implementation, the method gets all the actors of the AUnitBase class in the game world and populates arrays AllUnits, FriendlyUnits, and EnemyUnitBases with the results. It also gets all the actors of the ANoPathFindingArea class in the game world and populates the NoPathFindingAreas array with the results.

```cpp
bool APathProviderHUD::IsLocationInNoPathFindingAreas(FVector Location)
```
This is a method that takes a FVector as an argument and returns a bool. It checks if the given location is inside any of the ANoPathFindingArea actors previously added to the NoPathFindingAreas array. If it is, it returns true, otherwise it returns false.

```cpp
void APathProviderHUD::CreateGridsfromDataTable()
```
This is a method that populates the PathMatrixes array with FPathMatrix structures created from data in a GridDataTable. The GridDataTable must have been previously set.

```cpp
void APathProviderHUD::CreateGridAndDijkstra()
```
This method populates the G_DijkstraPMatrixes array with FDijkstraMatrix structures created by running the Dijkstra algorithm on each of the PathMatrixes. It also associates each FDijkstraMatrix with a ADijkstraCenter actor in the game world. Both the PathMatrixes array and the ADijkstraCenter actors array must have been previously populated.

```cpp
void APathProviderHUD::Tick(float DeltaSeconds)
```
This method overrides the Tick method of the AActor class. It is called every frame by the game engine. In this implementation, it updates a timer and when it reaches a certain value, it calls the CreateGridAndDijkstra method to populate the G_DijkstraPMatrixes array. It also calls other methods to move and patrol the friendly and enemy units through waypoints.

```cpp
void APathProviderHUD::SetNextDijkstra(TArray<AUnitBase*> Units, float DeltaSeconds)
```
This method updates the Next_DijkstraPMatrixes field of each of the AUnitBase actors in the given Units array. The Next_DijkstraPMatrixes field is set to the FDijkstraMatrix in the G_DijkstraPMatrixes array that is closest to the AUnitBase actor in terms of Euclidean distance. The method does this by running a search of the G_DijkstraPMatrixes array for the closest one, and then updating the Next_DijkstraPMatrixes field of the AUnitBase actor accordingly. The method is called every SetNextDijkstraPauseTime seconds, as specified by the class member variable.

Note that the code contains additional helper methods such as CreatePathMatrix and Dijkstra that are not shown in the provided code snippet.


Verwendete Bibliotheken
Der Code verwendet folgende Unreal Engine Bibliotheken:

"Hud/PathProviderHUD.h"
"Kismet/GameplayStatics.h"
"Math/UnrealMathUtility.h"
"Characters/UnitBase.h"
"Algo/Reverse.h"







Here's a list of the properties (variables) in the `APathProviderHUD` class and what they are used for:

-   `TraceChannelProperty`: Used to specify the collision channel for the trace that the class performs.
-   `QueryParams`: Used to hold the parameters for a collision query.
-   `MaxCosts`: Maximum cost for a path in the Dijkstra algorithm.
-   `MaxDistance`: Maximum distance for a path in the Dijkstra algorithm.
-   `Debug`: Whether or not to show debug information in the HUD.
-   `StopLoading`: Whether or not to stop loading.
-   `DisablePathFindingOnEnemy`: Whether or not to disable pathfinding on enemy units.
-   `DisablePathFindingOnFriendly`: Whether or not to disable pathfinding on friendly units.
-   `PathMatrixes`: An array of `FPathMatrix` structures.
-   `FoundCenterPoints`: An array of `AActor` objects that represent the center points for the grid.
-   `GridDataTable`: A reference to a `UDataTable` object that holds the data for the grid.
-   `CreatedGridAndDijkstra`: Whether or not the grid and Dijkstra algorithm have been created.
-   `SetNextDijkstraPauseTime`: The time to wait before the next Dijkstra algorithm is calculated in real-time.

In addition, the class also has several functions that use these properties to perform various actions, such as creating the grid for Dijkstra, calculating Dijkstra in `Begin_Play`, and handling the Dijkstra matrix.
