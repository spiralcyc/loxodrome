Arctic Research Station drone model (structure from motion)
===========================================================

Open index.html in Chrome, Safari or Firefox. It runs offline, and no server is needed.

Controls
  Drag = orbit, right-drag = pan, scroll = zoom, double-click = fly to a point

export/
  fmars_sfm_mesh.glb               Textured mesh, 2.5 M triangles, 8192 px textures (Blender, QGIS 3D, Cesium, three.js).
                                   glTF axes: x = East, y = Up, z = -North, in metres, in a local frame.
                                   The origin lat/lon and base elevation are in the file's asset.extras.
  fmars_sfm_dem_0p5m_utm16n.tif    DEM, 0.5 m, EPSG:32616 (WGS84 / UTM 16N). Nodata = -9999.

Processing
  1,141 DJI M3T wide-camera frames (4 flights, 10-11 July 2026, ~91 m AGL), downsampled to 2000x1500.
  COLMAP/GLOMAP SfM with GPS-guided matching. Bundle adjustment with GPS position priors plus a constant
  barometric altitude per flight, which removes the ~9 m "doming" of nadir grids. OpenMVS depth maps were
  fused into a 0.3 m DEM, meshed and textured from a covering subset of 376 images.

Accuracy
  No ground control. Horizontal position matches the drone GPS to ~0.6 m RMS (absolute accuracy: a couple of
  metres). Elevations are in the drone's GPS altitude datum, so treat absolute heights as +/- several m.
  Relative heights are much better: multi-view depth agreement ~2 cm median, camera heights 0.35 m RMS.
  The surface is 2.5D (a height field), so vertical walls such as the habitat are draped rather than modelled.
  Ponds and snow without texture are interpolated.
