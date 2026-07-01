<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no" />
    <title>Polar Bear Tracking — Ursula (X32465)</title>
    <script type="module" src="https://js.arcgis.com/5.0/"></script>
    <style>
      html, body {
        margin: 0;
        padding: 0;
        height: 100%;
        width: 100%;
        background: #1a1a2e;
        font-family: sans-serif;
      }
      calcite-shell {
        --calcite-color-brand: #5bc8d8;
      }
      #header {
        padding: 12px 16px;
        background: #1a1a2e;
        color: #f5fbff;
      }
      #heading {
        font-size: 20px;
        font-weight: 600;
        color: #f5fbff;
      }
      #subheading {
        font-size: 13px;
        color: #8a9baa;
        margin-top: 2px;
      }
      arcgis-map {
        height: calc(100vh - 130px);
        display: block;
      }
    </style>
  </head>

  <body class="calcite-mode-dark">
    <calcite-shell>
      <div slot="header" id="header">
        <div id="heading">🐻‍❄️ Polar Bear Tracking — Ursula (X32465)</div>
        <div id="subheading">GPS locations from Oct 2025 – Apr 2026 · Hudson Bay region, Canada</div>
      </div>

      <arcgis-map id="mapEl">
        <arcgis-zoom slot="top-left"></arcgis-zoom>
        <arcgis-home slot="top-left"></arcgis-home>
      </arcgis-map>

      <calcite-shell-panel slot="panel-bottom" display-mode="float">
        <arcgis-time-slider
          id="timeSlider"
          layout="auto"
          mode="cumulative-from-start"
          reference-element="mapEl"
          play-rate="600">
        </arcgis-time-slider>
      </calcite-shell-panel>
    </calcite-shell>

    <script type="module">
      const [WebMap, GeoJSONLayer] = await $arcgis.import([
        "@arcgis/core/WebMap.js",
        "@arcgis/core/layers/GeoJSONLayer.js"
      ]);

      // cleaned data — fixed Russia coordinate and swapped ref/time row
      const geojson = {
        type: "FeatureCollection",
        features: [
          { type: "Feature", geometry: { type: "Point", coordinates: [-91.37202, 61.193091] },    properties: { ref: "X19939", time: "2026-04-23T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-90.007269, 60.810576] },   properties: { ref: "X19939", time: "2026-04-20T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-90.007655, 61.038746] },   properties: { ref: "X19939", time: "2026-04-17T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-89.588115, 61.810804] },   properties: { ref: "X19939", time: "2026-04-14T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-89.64767, 62.438173] },    properties: { ref: "X19939", time: "2026-04-07T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-89.369665, 62.175627] },   properties: { ref: "X19939", time: "2026-04-10T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-88.37935, 63.194856] },    properties: { ref: "X19939", time: "2026-04-03T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-88.17208, 63.032497] },    properties: { ref: "X19939", time: "2026-03-31T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-88.194332, 62.687618] },   properties: { ref: "X19939", time: "2026-03-27T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-88.317853, 62.682479] },   properties: { ref: "X19939", time: "2026-03-23T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-88.252879, 62.24529] },    properties: { ref: "X19939", time: "2026-03-20T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-90.043039, 62.147282] },   properties: { ref: "X19939", time: "2026-03-16T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-90.45876, 62.04009] },     properties: { ref: "X19939", time: "2026-03-13T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-91.129419, 61.79882] },    properties: { ref: "X19939", time: "2026-03-09T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-90.96853, 61.374055] },    properties: { ref: "X19939", time: "2026-03-05T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-91.311627, 61.696939] },   properties: { ref: "X19939", time: "2026-03-01T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-91.792343, 61.806673] },   properties: { ref: "X19939", time: "2026-02-27T00:00:00Z" } },
          // skipped bad Russia coordinate row (2026-02-23)
          { type: "Feature", geometry: { type: "Point", coordinates: [-92.882854, 60.664106] },   properties: { ref: "X19939", time: "2026-02-21T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-92.493687, 59.330233] },   properties: { ref: "X19939", time: "2026-02-17T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-90.619585, 59.383126] },   properties: { ref: "X19939", time: "2026-02-12T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-89.217605, 59.212827] },   properties: { ref: "X19939", time: "2026-02-09T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-88.783945, 59.210574] },   properties: { ref: "X19939", time: "2026-02-05T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-88.977976, 59.285268] },   properties: { ref: "X19939", time: "2026-02-01T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-88.849778, 59.193054] },   properties: { ref: "X19939", time: "2026-01-30T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-87.766036, 59.064705] },   properties: { ref: "X19939", time: "2026-01-26T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-87.073737, 58.095151] },   properties: { ref: "X19939", time: "2026-01-15T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-87.200713, 58.362846] },   properties: { ref: "X19939", time: "2026-01-12T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-86.306024, 58.102672] },   properties: { ref: "X19939", time: "2026-01-09T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-85.812208, 57.286347] },   properties: { ref: "X19939", time: "2026-01-05T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-86.43492, 57.265576] },    properties: { ref: "X19939", time: "2026-01-03T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-88.21654, 58.381814] },    properties: { ref: "X19939", time: "2025-12-29T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-88.082709, 58.057331] },   properties: { ref: "X19939", time: "2025-12-27T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-89.983451, 57.402475] },   properties: { ref: "X19939", time: "2025-12-23T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-91.695011, 57.612085] },   properties: { ref: "X19939", time: "2025-12-19T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-92.742274, 58.055636] },   properties: { ref: "X19939", time: "2025-12-16T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-93.3855, 57.600058] },     properties: { ref: "X19939", time: "2025-12-12T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-93.431602, 57.484261] },   properties: { ref: "X19939", time: "2025-12-07T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-93.431913, 57.484186] },   properties: { ref: "X19939", time: "2025-11-27T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-93.431913, 57.484186] },   properties: { ref: "X19939", time: "2025-11-24T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-93.431827, 57.484208] },   properties: { ref: "X19939", time: "2025-11-20T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-93.431473, 57.484218] },   properties: { ref: "X19939", time: "2025-11-12T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-93.431849, 57.484294] },   properties: { ref: "X19939", time: "2025-11-04T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-93.479378, 57.469938] },   properties: { ref: "X19939", time: "2025-10-31T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-93.497338, 57.462375] },   properties: { ref: "X19939", time: "2025-09-27T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-93.496469, 57.461838] },   properties: { ref: "X19939", time: "2025-09-20T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-93.3303, 57.347404] },     properties: { ref: "X19939", time: "2025-08-26T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-93.329732, 57.347297] },   properties: { ref: "X19939", time: "2025-08-13T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-93.32972, 57.347276] },    properties: { ref: "X19939", time: "2025-08-07T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-93.328841, 57.347705] },   properties: { ref: "X19939", time: "2025-07-24T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-93.310484, 57.376319] },   properties: { ref: "X19939", time: "2025-07-16T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-93.323187, 57.530492] },   properties: { ref: "X19939", time: "2025-07-13T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-91.130159, 58.876103] },   properties: { ref: "X19939", time: "2025-07-04T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-90.174778, 58.862144] },   properties: { ref: "X19939", time: "2025-06-30T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-90.706338, 58.387061] },   properties: { ref: "X19939", time: "2025-06-27T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-91.306359, 58.579804] },   properties: { ref: "X19939", time: "2025-06-24T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-91.242962, 59.064276] },   properties: { ref: "X19939", time: "2025-06-20T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-91.493416, 59.691945] },   properties: { ref: "X19939", time: "2025-06-17T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-92.880623, 60.006976] },   properties: { ref: "X19939", time: "2025-06-13T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-92.557696, 60.531766] },   properties: { ref: "X19939", time: "2025-06-09T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-91.92919, 60.609561] },    properties: { ref: "X19939", time: "2025-06-05T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-90.814903, 61.293213] },   properties: { ref: "X19939", time: "2025-06-02T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-90.643907, 61.21354] },    properties: { ref: "X19939", time: "2025-05-30T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-89.913788, 61.321709] },   properties: { ref: "X19939", time: "2025-05-26T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-89.154316, 60.891986] },   properties: { ref: "X19939", time: "2025-05-23T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-89.234514, 60.583457] },   properties: { ref: "X19939", time: "2025-05-19T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-89.139445, 60.516059] },   properties: { ref: "X19939", time: "2025-05-16T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-88.599431, 60.53536] },    properties: { ref: "X19939", time: "2025-05-12T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-88.456019, 60.739058] },   properties: { ref: "X19939", time: "2025-05-08T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-88.429905, 60.621405] },   properties: { ref: "X19939", time: "2025-05-02T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-89.132418, 60.400509] },   properties: { ref: "X19939", time: "2025-04-29T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-88.696505, 60.464324] },   properties: { ref: "X19939", time: "2025-04-24T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-88.282769, 60.756696] },   properties: { ref: "X19939", time: "2025-04-18T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-87.29916, 60.733189] },    properties: { ref: "X19939", time: "2025-04-14T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-85.828248, 60.653967] },   properties: { ref: "X19939", time: "2025-04-11T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-87.41721, 61.995415] },    properties: { ref: "X19939", time: "2025-04-07T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-88.537622, 61.415028] },   properties: { ref: "X19939", time: "2025-04-02T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-88.664888, 61.184519] },   properties: { ref: "X19939", time: "2025-03-31T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-88.852749, 61.076533] },   properties: { ref: "X19939", time: "2025-03-29T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-88.557824, 60.811992] },   properties: { ref: "X19939", time: "2025-03-25T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-89.929431, 60.711034] },   properties: { ref: "X19939", time: "2025-03-14T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-90.617074, 60.585238] },   properties: { ref: "X19939", time: "2025-03-10T00:00:00Z" } },
          // skipped malformed row (swapped ref/time, no date)
          { type: "Feature", geometry: { type: "Point", coordinates: [-91.499371, 60.090188] },   properties: { ref: "X19939", time: "2025-02-28T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-92.550496, 60.112397] },   properties: { ref: "X19939", time: "2025-02-24T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-92.080048, 59.90989] },    properties: { ref: "X19939", time: "2025-02-21T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-91.525678, 59.540142] },   properties: { ref: "X19939", time: "2025-02-17T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-90.686662, 59.351991] },   properties: { ref: "X19939", time: "2025-02-14T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-89.893232, 58.983445] },   properties: { ref: "X19939", time: "2025-02-10T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-90.001625, 58.887057] },   properties: { ref: "X19939", time: "2025-02-07T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-92.682686, 59.733616] },   properties: { ref: "X19939", time: "2025-01-30T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-92.255486, 60.344816] },   properties: { ref: "X19939", time: "2025-01-26T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-91.804027, 61.009811] },   properties: { ref: "X19939", time: "2025-01-23T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-91.626143, 61.841939] },   properties: { ref: "X19939", time: "2025-01-16T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-91.175339, 61.34175] },    properties: { ref: "X19939", time: "2025-01-10T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-90.336462, 60.534158] },   properties: { ref: "X19939", time: "2025-01-06T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-93.952659, 59.852673] },   properties: { ref: "X19939", time: "2024-12-06T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-94.430349, 59.018013] },   properties: { ref: "X19939", time: "2024-11-29T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-93.295764, 58.436521] },   properties: { ref: "X19939", time: "2024-11-22T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-92.915813, 58.053265] },   properties: { ref: "X19939", time: "2024-11-08T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-93.490868, 57.367467] },   properties: { ref: "X19939", time: "2024-10-26T00:00:00Z" } },
          { type: "Feature", geometry: { type: "Point", coordinates: [-93.491662, 57.354496] },   properties: { ref: "X19939", time: "2024-10-11T00:00:00Z" } }
        ]
      };

      const blob = new Blob([JSON.stringify(geojson)], { type: "application/json" });
      const url = URL.createObjectURL(blob);

      const layer = new GeoJSONLayer({
        url: url,
        timeInfo: {
          startField: "time",
          trackIdField: "ref"
        },
        trackInfo: {
          enabled: true,
          maxDisplayObservationsPerTrack: 0,
          latestObservations: {
            visible: true,
            renderer: {
              type: "simple",
              symbol: {
                type: "simple-marker",
                color: [250, 247, 242],
                size: 12,
                outline: { color: [91, 200, 216], width: 2 }
              }
            }
          },
          previousObservations: {
            visible: true,
            renderer: {
              type: "simple",
              symbol: {
                type: "simple-marker",
                color: [91, 200, 216],
                size: 6,
                outline: { color: [250, 247, 242], width: 1 }
              }
            }
          },
          trackLines: {
            visible: true,
            renderer: {
              type: "simple",
              symbol: {
                type: "simple-line",
                color: [91, 200, 216, 200],
                width: 2
              }
            }
          }
        },
        popupTemplate: {
          title: "Ursula (X32465)",
          content: "Date: {time}"
        }
      });

      const mapEl = document.getElementById("mapEl");
      const timeSlider = document.getElementById("timeSlider");

      // Load WebMap first, then add bear layer on top of ice layer
      const webmap = new WebMap({
        portalItem: {
          id: "2e95726e9331460089876d513e73913b",
          portal: { url: "https://smartnorth.maps.arcgis.com" }
        }
      });

      await webmap.load();
      webmap.add(layer); // added last = renders on top of ice layer
      mapEl.map = webmap;

      // Set time slider extents to match full data range
      timeSlider.fullTimeExtent = {
        start: new Date("2025-10-31"),
        end: new Date("2026-04-24")
      };
      timeSlider.timeExtent = {
        start: new Date("2025-10-31"),
        end: new Date("2025-10-31")
      };
      timeSlider.stops = {
        interval: { value: 7, unit: "days" }
      };

      // zoom to data on load
      mapEl.addEventListener("arcgisViewReadyChange", () => {
        mapEl.goTo({
          center: [-90.5, 58.0],
          zoom: 6
        });
      });
    </script>
  </body>
</html># UsulaPolarBear
