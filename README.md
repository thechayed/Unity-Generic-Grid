# Unity-Generic-Grid
A flexible Grid Data Structure for Unity with a myriad of search methods and Unity Events, built on top of the Unity Generic Item Collection.

## Install
You can Install it via the .UnityPackage in releases, but the .zip may have features not yet included in the package.

## Use
You can use Grids in one of two ways, either create a Grid Field/Property, or implement the IGrid Interface, where standard implementations for methods for accessing the Grid are kept. 

## Features
- Extends my ItemCollection script, which itself extends from List<T> to provide some extra bits and bobs. Chech it's Github page here for more info:
- Uses it's Width and Height to access GridNodes (the Items of its List) for setting and getting values
``` c#
// Creates a new Grid, and get's the Grid Node at the given position, then accesses the Node's Value.
var grid = new Grid<string>(5,10);
var item = grid[2, 7];
item.value = "Hello, World";
var value = item.value;

// You can also use this Methods to Get/Set the Value of the GridNode at the given Position
value = grid.GetValue(2, 7);
value = grid.SetValue(2, 7);
```
- Unity Events are triggers for Adding, Removing, or Moving values in the Grid.
- You can Move Grid Nodes
``` c#
// Move the Value at x:2, y:7 to x:3, y:9
grid.MoveValueAtPositionToPosition(2, 7, 3, 9);

// Finds value in the Grid and moves it to position x:3, y:9
grid.MoveValueToPosition(value, 3, 9);
```
- You can search the Grid for Values
``` c#
// Gets an X, Y position Tuple for the Node with the given Value
// (given everything previously done, the Tuple Values will be x:3, y:9) and sets local x and y values to the Tuple values.
var position = grid.GetPositionOf(value);
var x = position.x;
var y = position.y;

// You can get nodes using search methods 
var relativeRow = grid.GetRow(y);
relativeRow(item.y);
var relativeColumn = grid.GetColumn(x);

relativeColumn(item.x);
var adjacentNodes = grid.GetAdjacentNodes(x, y);

var range = 10;
var rangeOfNodes = grid.GetRange(x, y, range);

// You can also use Predicates.
var predicate = item => item.value.StartsWith("H");

var predicateRow = grid.GetRowMatchingPredicate(y, predicate);
var predicateColumn = grid.GetColumnMatchingPredicate(x, predicate);
var predicateAdjacent = grid.GetAdjacentMathcingPredicate(x, y, predicate);
var predicateRange = grid.GetRangeMatchingPredicate(x, y, range, predicate);

// Finally, you can search iteratively for values based on a predicate,
// starting from the position, and continuing until the conditions of the predicate are not met for any of the relative Nodes.
var searchdNodes = grid.SearchFromPointMatchingPredicate(x, y, predicate);
```
