# PathFinder_ReadMe
Documentation for a Unreal Engine Plugin


Code-Dokumentation: APathProviderHUD
Die APathProviderHUD ist eine Blueprint-Klasse, die von der Klasse AHUD erbt. Es ist eine Basisklasse für HUD-Elemente, die Pfadfindungslogik benötigen. Der folgende Code dokumentiert die Methoden der Klasse.

```cpp
void APathProviderHUD::BeginPlay()
```
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
