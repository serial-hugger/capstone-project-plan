# capstone-project-plan
[[[ OVERVIEW ]]]

---[SUMMARY]

----An web frontend that when you enter a coordinate it draws a map
----of the roads, buildings, bodies of water and forestry of that area
----and displays generated spawn points that could be used for a game.

---[FEATURES]

----UI that accepts coordinates and a pane that the map will be drawn.

----Project API that can query external api for map information and store
----it in the internal database.

[[[ TECHNICAL ]]]

---[TOOLS]

----OpenStreetMap to get map info.

----S2Geometry to make map info, spawn points and distance measurements
----more managable.

----Sqlite for internal database.

---[DETAILS]

----S2Geometry is an algorithm that makes using coordinate data easier by
----mapping a grid of cells as a flat representation of the earths globe.

----S2Geometry has different levels of cells, the higher the level is the
----smaller the size of the cells. Level 15 (~200 - 300 meters) will be
----used for storing the information in the internal database. The map will
----be drawn at level 10 (~ 7 - 10 kilometer).

[[[ PLAN OUTLINE ]]]

----Whenever user submits the coordinate, send it to the projects API.

----Whenever the project API recieves the coordinates it will first figure
----out what level 10 cell the coordinate is in and will query OpenStreetMap
----for information within that cell if it's not already stored.

----Whenever the project API recieves the OpenStreetMap information at level 10
----it will then create the geometry and split it into level 15 and save them to
----the database as JSON.

----If the information has already been stored it will return all stored level 15
----cells from the database.

----The API will then respond with information needed to draw the map.

----The UI will then draw the map in the pane.

[[[ DOWNSIZE PLAN ]]]

----Draw the map with level 10 data from OpenStreetMap rather than storing the
----information in own database, and instead only use internal database for storing
----spawn points.
