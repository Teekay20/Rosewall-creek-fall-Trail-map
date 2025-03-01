import "leaflet/dist/leaflet.css";
import "./styles.css";
import {
  MapContainer,
  TileLayer,
  Marker,
  Popup,
  Polyline,
  LayersControl,
  useMap,
} from "react-leaflet";
import L from "leaflet";
import { useEffect, useState } from "react";
import * as toGeoJSON from "@tmcw/togeojson";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faLayerGroup } from "@fortawesome/free-solid-svg-icons";
import { GeoSearchControl, OpenStreetMapProvider } from "leaflet-geosearch";

// Destructure BaseLayer from LayersControl
const { BaseLayer } = LayersControl;

// Search Bar Component
const SearchBar = () => {
  const map = useMap();

  useEffect(() => {
    const provider = new OpenStreetMapProvider();
    const searchControl = new GeoSearchControl({
      provider,
      style: "bar",
      autoComplete: true,
      autoCompleteDelay: 250,
      showMarker: true,
      retainZoomLevel: false,
      animateZoom: true,
    });

    map.addControl(searchControl);

    return () => {
      map.removeControl(searchControl);
    };
  }, [map]);

  return null;
};

// Legend Component
const Legend = ({ isLegendVisible, icons, trackLine }) => {
  const map = useMap();

  useEffect(() => {
    if (!isLegendVisible) return;

    const legend = L.control({ position: "bottomright" });

    legend.onAdd = () => {
      const div = L.DomUtil.create("div", "info legend");
      div.style.backgroundColor = "white";
      div.style.padding = "12px";
      div.style.borderRadius = "8px";
      div.style.boxShadow = "0 4px 10px rgba(0, 0, 0, 0.3)";
      div.style.fontSize = "14px";
      div.style.bottom = "50px";

      div.innerHTML = `
        <h4 style="margin: 0 0 10px; text-align: center;">Legend</h4>
        <div style="display: flex; flex-direction: column; gap: 8px;">
          ${Object.entries(icons)
            .map(
              ([key, icon]) => `
                <div style="display: flex; align-items: center; gap: 10px;">
                  <img src="${
                    icon.options.html.match(/src="([^"]+)"/)[1]
                  }" width="30" height="30" />
                  <span style="font-size: 15px; font-weight: bold;">${key}</span>
                </div>
              `
            )
            .join("")}
          <div style="display: flex; align-items: center; gap: 10px;">
            <div style="
              width: 40px; 
              height: 5px; 
              background-color: white; 
              border: 3px dashed white; 
              box-shadow: 0px 0px 3px 3px black;">
            </div>
            <span style="font-size: 15px; font-weight: bold;">Trail</span>
          </div>
        </div>
      `;

      return div;
    };

    legend.addTo(map);

    return () => {
      legend.remove();
    };
  }, [map, isLegendVisible, icons, trackLine]);

  return null;
};

// Define createCircularIcon function
const createCircularIcon = (iconUrl) => {
  return L.divIcon({
    className: "circular-icon",
    html: `<img src="${iconUrl}" alt="Icon" 
      style="width: 60px; height: 60px; border-radius: 50%; 
      object-fit: cover; border: 2px solid white; 
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);" />`,
    iconSize: [60, 60],
    iconAnchor: [30, 30],
  });
};

// Define all icons
const hikingIcon = createCircularIcon(
  "https://img.freepik.com/premium-photo/person-walking-toward-horizon-peaceful-landscape_734790-18935.jpg"
);
const fallIcon = createCircularIcon(
  "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcS0eV14PfKgddIdB8FGLVvo6My81HXL5YbUuQ44vyyg_cIz2g1hktMUqPOwju0J6grOdBE&usqp=CAU"
);
const riverIcon = createCircularIcon(
  "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRx1mzToMGIRWH2ZJ6eYqonK8gvU6PD9nX4GxTMuioax7orKsSB7trJM0WW_Vr6ivdp-sA&usqp=CAU"
);
const bridgeIcon = createCircularIcon(
  "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQseRwqSY0P71v5gVvB7PsYJQzAijYRIJDhqpdUa6MyBIHTcfSr3ATWLbix2eOJY6iWbCQ&usqp=CAU"
);
const logIcon = createCircularIcon(
  "https://c8.alamy.com/comp/2AB0M1E/fallen-tree-crossing-a-hiking-trail-in-autumn-at-nature-reserve-leudal-province-noord-limburg-netherlands-2AB0M1E.jpg"
);
const steepIcon = createCircularIcon(
  "https://media.compliancesigns.com/media/catalog/product/t/r/trail-sign-nhe-17512_1000.gif"
);
const parkingIcon = createCircularIcon(
  "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSBIROw-nRsgPFwb2X14G25fAg3ljxDpyWhow&s"
);
const picnicIcon = createCircularIcon(
  "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQQkebYAb8IZxdj-BGLa_xEKhqqTNuzVhtTkg&s"
);
const highwayIcon = createCircularIcon(
  "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcREPDcFw92kMubir5EmVdjgsTMYQRljSGANmQ&s"
);
const obstacleIcon = createCircularIcon(
  "https://thumbs.dreamstime.com/b/running-obstacles-vector-icon-golden-circle-cartoon-style-isolated-white-background-81122715.jpg"
);
const treeIcon = createCircularIcon(
  "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSHLQ-Ob8VPjQyDbERhVSCku4V5hglwStne7Q&s"
);

// Define image and elevation data for each waypoint
const waypointImagesAndElevations = {
  "Therriault Upper Falls": {
    image:
      "https://www.shutterstock.com/image-photo/therriault-falls-near-mud-bay-600w-1148752859.jpg",
    elevation: "130m",
  },
  "Upper Falls Area": {
    image: "https://s0.wklcdn.com/image_28/843187/138375653/87852606Master.jpg",
    elevation: "131m",
  },
  Trail: {
    image: "https://s2.wklcdn.com/image_28/843187/138375654/87852683Master.jpg",
    elevation: "114m",
  },
  "Cross the brook below or walk the log": {
    image:
      "https://s0.wklcdn.com/image_28/843187/138375655/87852747.700x525.jpg",
    elevation: "112m",
  },
  "Steep Upper Trail Area": {
    image:
      "https://s2.wklcdn.com/image_28/843187/138375656/87852782.700x525.jpg",
    elevation: "109m",
  },
  "Steep Trail": {
    image:
      "https://s2.wklcdn.com/image_28/843187/138375657/87852824.700x525.jpg",
    elevation: "107m",
  },
  "Therriault Upper Falls from Approach": {
    image:
      "https://s0.wklcdn.com/image_28/843187/138375658/87852858.400x300.jpg",
    elevation: "100m",
  },
  "Terriault Lower Falls": {
    image: "https://s0.wklcdn.com/image_28/843187/138375659/87852936Master.jpg",
    elevation: "94m",
  },
  "Another Decent Picnic or Bathing Spot": {
    image:
      "https://s1.wklcdn.com/image_28/843187/138375660/87853045.700x525.jpg",
    elevation: "91m",
  },
  "A Pleasant Stretch of Trail": {
    image: "https://s2.wklcdn.com/image_28/843187/138375661/87853112Master.jpg",
    elevation: "85m",
  },
  "Trail and View to the River": {
    image: "https://s2.wklcdn.com/image_28/843187/138375662/87853139Master.jpg",
    elevation: "78m",
  },
  "Hollow Tree": {
    image: "https://s0.wklcdn.com/image_28/843187/138375663/87853218Master.jpg",
    elevation: "85m",
  },
  "A Decent Trail...until that fallen log across it": {
    image: "https://s2.wklcdn.com/image_28/843187/138375664/87853250Master.jpg",
    elevation: "64m",
  },
  "Some Fallen Logs are easy to duck under": {
    image:
      "https://s1.wklcdn.com/image_28/843187/138375665/87853297.400x300.jpg",
    elevation: "72m",
  },
  "A Bridge Across the River...for the daring": {
    image: "https://s2.wklcdn.com/image_28/843187/138375666/87853322Master.jpg",
    elevation: "62m",
  },
  "A Log to Step Over": {
    image: "https://s1.wklcdn.com/image_28/843187/138375667/87853402Master.jpg",
    elevation: "59m",
  },
  "A Narrow View to the River": {
    image: "https://s1.wklcdn.com/image_28/843187/138375668/87853441Master.jpg",
    elevation: "41m",
  },
  "This Log on the trail has a cut-out!": {
    image:
      "https://s2.wklcdn.com/image_28/843187/138375669/87853493.700x525.jpg",
    elevation: "38m",
  },
  "Tree with Fungus": {
    image: "https://s2.wklcdn.com/image_28/843187/138375670/87853505Master.jpg",
    elevation: "39m",
  },
  "Trail with Drop-Off on the River Side": {
    image: "https://s1.wklcdn.com/image_28/843187/138375671/87853519Master.jpg",
    elevation: "39m",
  },
  "Another log to Step over": {
    image: "https://s1.wklcdn.com/image_28/843187/138375672/87853540Master.jpg",
    elevation: "36m",
  },
  "River's Edge": {
    image: "https://s2.wklcdn.com/image_28/843187/138375673/87853583Master.jpg",
    elevation: "33m",
  },
  "Easy Trail Area": {
    image:
      "https://s1.wklcdn.com/image_28/843187/138375674/87853615.700x525.jpg",
    elevation: "27m",
  },
  "Some Roots on the Trail": {
    image:
      "https://s2.wklcdn.com/image_28/843187/138375675/87853655.700x525.jpg",
    elevation: "22m",
  },
  "Tree Canopy": {
    image:
      "https://s0.wklcdn.com/image_28/843187/138375676/87853683.700x525.jpg",
    elevation: "27m",
  },
  "A Few Trail Obstacles": {
    image:
      "https://s0.wklcdn.com/image_28/843187/138375677/87853722.400x300.jpg",
    elevation: "24m",
  },
  "Open Area on Trail": {
    image: "https://s0.wklcdn.com/image_28/843187/138375678/87853767Master.jpg",
    elevation: "22m",
  },
  "Another Natural Bridge...for the Brave": {
    image: "https://s2.wklcdn.com/image_28/843187/138375679/87853778Master.jpg",
    elevation: "21m",
  },
  "A Swimming Hole? Watch the Current": {
    image:
      "https://s1.wklcdn.com/image_28/843187/138375680/87853834.400x300.jpg",
    elevation: "19m",
  },
  "Lower River": {
    image: "https://s0.wklcdn.com/image_28/843187/138375681/87853848Master.jpg",
    elevation: "19m",
  },
  "Walking under Highway 19": {
    image: "https://s1.wklcdn.com/image_28/843187/138375682/87853897Master.jpg",
    elevation: "18m",
  },
  "Walking under the smaller Highway 19A": {
    image: "https://s1.wklcdn.com/image_28/843187/138375683/87853972Master.jpg",
    elevation: "16m",
  },
  "Picnic Area in Rosewall Creek Park": {
    image:
      "https://s1.wklcdn.com/image_28/843187/138375684/87854053.700x525.jpg",
    elevation: "16m",
  },
  "Parking Area at Rosewall Creek Provincial Park": {
    image: "https://s0.wklcdn.com/image_28/843187/138375685/87854076Master.jpg",
    elevation: "16m",
  },
};

// Define icons for the legend
const icons = {
  Hiking: hikingIcon,
  WaterFall: fallIcon,
  River: riverIcon,
  Bridge: bridgeIcon,
  Log: logIcon,
  Steep_Area: steepIcon,
  Car_Park: parkingIcon,
  Picnic_Area: picnicIcon,
  Highway: highwayIcon,
  Risk: obstacleIcon,
  Tree: treeIcon,
};

// Component to add Scale Bar
const MapEnhancements = ({ trackLine }) => {
  const map = useMap();

  useEffect(() => {
    if (!map || trackLine.length === 0) return;

    // Remove existing scale bar if it already exists
    const existingScaleBar = document.querySelector(".leaflet-control-scale");
    if (!existingScaleBar) {
      L.control.scale({ position: "bottomleft" }).addTo(map);
    }
  }, [map, trackLine]);

  return null;
};

// Main App Component
const App = () => {
  const [trackLine, setTrackLine] = useState([]);
  const [waypoints, setWaypoints] = useState([]);
  const [isLegendVisible, setIsLegendVisible] = useState(false);

  // Fetch GPX data and process it
  useEffect(() => {
    fetch("/rosewall-creek-to-therriault-falls.gpx")
      .then((response) => response.text())
      .then((gpxText) => {
        const parser = new DOMParser();
        const gpx = parser.parseFromString(gpxText, "application/xml");
        const geojson = toGeoJSON.gpx(gpx);

        // Extract Track Points
        if (geojson.features.length > 0) {
          const trackPoints = geojson.features
            .filter((feature) => feature.geometry.type === "LineString")
            .flatMap((feature) =>
              feature.geometry.coordinates.map((coord) => [coord[1], coord[0]])
            );
          setTrackLine(trackPoints);
        }

        // Extract Waypoints
        const waypointFeatures = geojson.features.filter(
          (feature) => feature.geometry.type === "Point"
        );

        const waypointData = waypointFeatures.map((feature) => {
          const name = feature.properties.name || "Unnamed Waypoint";
          const details = waypointImagesAndElevations[name] || {};

          return {
            position: [
              feature.geometry.coordinates[1],
              feature.geometry.coordinates[0],
            ],
            name: name,
            elevation: details.elevation || "Unknown",
            image: details.image || "https://via.placeholder.com/150",
          };
        });

        setWaypoints(waypointData);
      })
      .catch((error) => console.error("Error loading GPX file:", error));
  }, []);

  return (
    <div>
      {/* Legend Toggle Button */}
      <button
        onClick={() => setIsLegendVisible(!isLegendVisible)}
        style={{
          position: "absolute",
          top: "80px",
          left: "10px",
          zIndex: 1000,
          padding: "12px",
          backgroundColor: "white", // Set background to white
          border: "none",
          borderRadius: "10%",
          cursor: "pointer",
          boxShadow: "0 4px 6px rgba(0, 0, 0, 0.3)",
          width: "30px",
          height: "30px",
          display: "flex",
          justifyContent: "center",
          alignItems: "center",
        }}
      >
        <img
          src={
            isLegendVisible
              ? "https://static.thenounproject.com/png/250120-200.png" // Toggle icon when legend is open
              : "https://cdn-icons-png.flaticon.com/512/447/447031.png" // Default icon
          }
          alt="Legend Toggle"
          style={{
            width: "20px",
            height: "20px",
            transition: "transform 0.3s ease-in-out",
          }}
        />
      </button>

      {/* Map Container */}
      <div
        style={{
          height: "100vh",
          width: "100%",
        }}
      >
        <MapContainer
          center={[49.4535, -124.8]}
          zoom={15}
          style={{ height: "100%", width: "100%" }}
        >
          {/* Add Legend */}
          <Legend
            isLegendVisible={isLegendVisible}
            icons={icons}
            trackLine={trackLine}
          />

          {/* Add MapEnhancements component */}
          <MapEnhancements trackLine={trackLine} />

          {/* Basemap Layer Control */}
          <LayersControl position="topright" collapsed={false}>
            {/* Map Group */}
            <LayersControl.Overlay name="Map" checked>
              <BaseLayer checked name="OpenStreetMap">
                <TileLayer
                  url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
                  attribution="&copy; OpenStreetMap contributors"
                />
              </BaseLayer>
              <BaseLayer name="Google Terrain">
                <TileLayer
                  url="https://mt1.google.com/vt/lyrs=p&x={x}&y={y}&z={z}"
                  attribution="&copy; Google"
                />
              </BaseLayer>
            </LayersControl.Overlay>

            {/* Satellite Group */}
            <LayersControl.Overlay name="Satellite">
              <BaseLayer name="Esri Satellite">
                <TileLayer
                  url="https://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}"
                  attribution="&copy; Esri, Maxar, Earthstar Geographics, and the GIS User Community"
                />
              </BaseLayer>
              <BaseLayer name="Google Satellite">
                <TileLayer
                  url="https://mt1.google.com/vt/lyrs=y&x={x}&y={y}&z={z}"
                  attribution="&copy; Google"
                />
              </BaseLayer>
            </LayersControl.Overlay>
          </LayersControl>

          {/* Render Track Line */}
          <Polyline
            positions={trackLine}
            color="white"
            weight={6}
            opacity={0.9}
            lineCap="round"
            lineJoin="round"
            dashArray="10, 10"
          />

          {/* Render Waypoints */}
          {waypoints.map((waypoint, index) => (
            <Marker
              key={index}
              position={waypoint.position}
              icon={
                waypoint.name.toLowerCase().includes("log") ||
                waypoint.name.toLowerCase().includes("logs") ||
                waypoint.name.toLowerCase().includes("fallen log") ||
                waypoint.name.toLowerCase().includes("fallen logs")
                  ? logIcon
                  : waypoint.name.toLowerCase().includes("fall")
                  ? fallIcon
                  : waypoint.name.toLowerCase().includes("river")
                  ? riverIcon
                  : waypoint.name.toLowerCase().includes("bridge")
                  ? bridgeIcon
                  : waypoint.name.toLowerCase().includes("steep")
                  ? steepIcon
                  : waypoint.name.toLowerCase().includes("parking")
                  ? parkingIcon
                  : waypoint.name.toLowerCase().includes("picnic")
                  ? picnicIcon
                  : waypoint.name.toLowerCase().includes("highway")
                  ? highwayIcon
                  : waypoint.name.toLowerCase().includes("obstacle")
                  ? obstacleIcon
                  : waypoint.name.toLowerCase().includes("tree")
                  ? treeIcon
                  : hikingIcon
              }
            >
              <Popup>
                <div
                  style={{
                    textAlign: "center",
                    maxWidth: "300px",
                    padding: "10px",
                  }}
                >
                  <strong style={{ fontSize: "16px" }}>{waypoint.name}</strong>
                  <br />
                  <span
                    style={{
                      fontSize: "14px",
                      fontWeight: "bold",
                      color: "#555",
                    }}
                  >
                    Elevation: {waypoint.elevation}
                  </span>
                  <br />
                  <img
                    src={waypoint.image}
                    alt={waypoint.name}
                    style={{
                      width: "100%",
                      height: "200px",
                      objectFit: "cover",
                      borderRadius: "10px",
                      marginTop: "8px",
                      border: "3px solid #ddd",
                      boxShadow: "0px 4px 10px rgba(0, 0, 0, 0.3)",
                    }}
                  />
                </div>
              </Popup>
            </Marker>
          ))}
        </MapContainer>
      </div>
    </div>
  );
};

export default App;
