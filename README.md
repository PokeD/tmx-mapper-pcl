# PCL Tiled Map File Parser 
TMXParserPCL is C# library for parsing Tiled Map's TMX files.

## Usage:
```csharp
// -- Load a file ho you want in PCL
var fileStream = File.Open("map.tmx", FileMode.Open);
// -- Load a file ho you want in PCL

var map = Map.Load(fileStream);


// If TileSet is an external file
var loadedExternalTileSets = new List<TileSet>();
var loadedImages = new List<Bitmap>();
foreach (var tileSet in map.TileSets)
{
  // -- Load a file ho you want in PCL
  var fileStream = File.Open(tileSet.Source, FileMode.Open);
  // -- Load a file ho you want in PCL
  
  var firstGID = tileSet.FirstGID;
  var serializer = new XmlSerializer(typeof(TileSet));
  var tileSetLoaded = (TileSet) serializer.Deserialize(fileStream);
  tileSetLoaded.FirstGID = firstGID;

  // -- Load a file ho you want in PCL
  var pictureStream = File.Open(tileSet.Image.Source, FileMode.Open);
  // -- Load a file ho you want in PCL
  var picture = new Bitmap(pictureStream);
  loadedImages.Add(picture);

  loadedExternalTileSets.Add(tileSetLoaded);
}
```
