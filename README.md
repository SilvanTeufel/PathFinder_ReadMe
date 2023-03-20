# PathFinder_ReadMe
Documentation for a Unreal Engine Plugin


Code-Dokumentation: APathProviderHUD
Die APathProviderHUD ist eine Blueprint-Klasse, die von der Klasse AHUD erbt. Es ist eine Basisklasse für HUD-Elemente, die Pfadfindungslogik benötigen. Der folgende Code dokumentiert die Methoden der Klasse.

```cpp
void APathProviderHUD::BeginPlay()
```
Die Methode BeginPlay() wird beim Starten der Blueprint-Instanz aufgerufen und ist Teil des Lebenszyklus von Actor-Klassen. Sie ruft die Superklasse AHUD::BeginPlay() auf und initialisiert Arrays mit Einheiten, NoPathFindingAreas und erstellt Raster und Dijkstra-Matrizen.

cpp
Copy code
bool APathProviderHUD::IsLocationInNoPathFindingAreas(FVector Location)
Die Methode IsLocationInNoPathFindingAreas() gibt zurück, ob sich die übergebene Position in einem Bereich ohne Pfadfindung befindet.

cpp
Copy code
void APathProviderHUD::CreateGridsfromDataTable()
Die Methode CreateGridsfromDataTable() erstellt ein Raster aus den Daten, die in der Raster-Datentabelle enthalten sind. Es werden Rastermatrizen erzeugt und in einem Array gespeichert.

cpp
Copy code
void APathProviderHUD::CreateGridAndDijkstra()
Die Methode CreateGridAndDijkstra() ruft CreateGridsfromDataTable() auf und erstellt Dijkstra-Matrizen aus den erstellten Rastermatrizen und den gefundenen Zentrumspunkten.

cpp
Copy code
void APathProviderHUD::Tick(float DeltaSeconds)
Die Methode Tick() wird jeden Frame aufgerufen und ist Teil des Lebenszyklus von Actor-Klassen. Sie ruft MoveUnitsThroughWayPoints() auf, um freundliche Einheiten durch Wegpunkte zu bewegen. Wenn DisablePathFindingOnEnemy falsch ist, ruft sie auch PatrolUnitsThroughWayPoints() auf, um feindliche Einheiten durch Wegpunkte zu bewegen. Schließlich ruft es SetNextDijkstra() auf, um den nächsten Dijkstra für feindliche Einheiten zu setzen.

cpp
Copy code
void APathProviderHUD::SetNextDijkstra(TArray <AUnitBase*> Units, float DeltaSeconds)
Die Methode SetNextDijkstra() sucht nach dem nächsten Dijkstra-Pfad für jede übergebene Einheit und weist den Einheiten den entsprechenden Dijkstra zu.

Verwendete Bibliotheken
Der Code verwendet folgende Unreal Engine Bibliotheken:

"Hud/PathProviderHUD.h"
"Kismet/GameplayStatics.h"
"Math/UnrealMathUtility.h"
"Characters/UnitBase.h"
"Algo/Reverse.h"







Sure, here's a list of the properties (variables) in the `APathProviderHUD` class and what they are used for:

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
