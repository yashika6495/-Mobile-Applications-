# Experiment 11 — Google Maps SDK on Android

**Student:** Yashika Chaudhary
**USN:** 25MCAR0139

---

## 1. What this experiment is about

This experiment builds a small native Android application that embeds an
interactive map inside a Kotlin activity. The user can switch between map
types (Normal, Satellite, Hybrid), zoom in and out, and re-center the camera
on a point of interest. A branded "profile strip" at the bottom of the screen
identifies the student the build belongs to.

The point of the experiment is to show that an Android app can:

- host an external SDK (Google Play Services — Maps) inside its own layout,
- react to user input (buttons, pills) and translate it into map API calls,
- control the camera and overlays (markers, info windows) programmatically,
- apply Material 3 styling consistently across chrome, controls and content.

## 2. Concept and technology

| Area | Choice | Why |
| --- | --- | --- |
| Language | Kotlin (JVM target 11) | Modern, concise, first-class on Android. |
| UI toolkit | Android Views + Material 3 | Simple layout XML + `MaterialToolbar` and FABs. |
| Map engine | Google Maps SDK (`play-services-maps`) | Fragment-based `SupportMapFragment` embeds a `GoogleMap` instance. |
| Build system | Gradle (Kotlin DSL) + Version Catalog | Declarative dependencies via `libs.versions.toml`. |
| Secret handling | `local.properties` → manifest placeholder `${MAPS_API_KEY}` | Keeps the API key out of source control. |
| Target SDK | 36, min SDK 24 | Covers Android 7.0 and above. |

The `GoogleMap` object is obtained asynchronously through
`SupportMapFragment.getMapAsync { … }`. Camera moves use
`CameraUpdateFactory.newLatLngZoom` / `.zoomIn` / `.zoomOut`, and the Normal
/ Satellite / Hybrid pills call `map.mapType = …` with the matching constant.
A loading overlay is dismissed as soon as the `GoogleMap` is ready so the UI
is interactive even when tile rendering is delayed.

## 3. Scenario demonstrated

The build is pinned to **Lalbagh Botanical Garden, Bengaluru** at zoom 15.
On launch, a purple marker is dropped at the garden with an info-window
showing "Lalbagh Botanical Garden · Bengaluru, Karnataka". The user can:

1. tap **Satellite** or **Hybrid** to swap the base map,
2. tap **+** / **×** to zoom the camera,
3. tap the **re-center** FAB to animate the camera back to the pinned
   location.

A persistent profile strip at the bottom of the screen displays
"USN · 25MCAR0139 · Yashika Chaudhary", which satisfies the requirement that
at least one test case shows the student's USN and name — in this
submission, *every* test case does.

## 4. Folder and file structure

```
Experiment11/
├── build.gradle.kts              # Root Gradle config (plugins)
├── settings.gradle.kts           # Includes :app and version catalog
├── local.properties              # MAPS_API_KEY lives here (git-ignored)
├── gradle/
│   └── libs.versions.toml        # Dependency version catalog
├── screenshots/                  # Output + test-case screenshots
└── app/
    ├── build.gradle.kts          # App module: reads MAPS_API_KEY, deps
    └── src/main/
        ├── AndroidManifest.xml   # Permissions + <meta-data> for the key
        ├── java/com/example/experiment11/
        │   ├── MainActivity.kt   # Activity + map + UI wiring
        │   └── StudentProfile.kt # Per-student theme + USN flipper
        └── res/
            ├── layout/activity_main.xml       # Toolbar, chips, map card, FABs, profile strip
            ├── drawable/                      # Shapes for pill, card, avatar, overlay
            ├── values/{colors,strings,styles,themes}.xml
            └── values-night/themes.xml
```

Key files:

- `MainActivity.kt` — reads `StudentProfile.ACTIVE`, binds the toolbar,
  profile strip, chips and FABs, and loads the map in `bindMap()`.
- `StudentProfile.kt` — single source of truth for which student the build
  represents. Flip `ACTIVE = MAHEEP` ↔ `ACTIVE = YASHIKA` and the whole UI
  (title, colors, marker, strip) swaps.
- `activity_main.xml` — Material 3 toolbar, centered chip row, map card
  with rounded corners, FAB column, bottom profile strip.

## 5. Output

![Output — Yashika variant](screenshots/25MCAR0139_output.png)

Title bar shows "Maps · 25MCAR0139 / Yashika Chaudhary". The map area is
pinned to Lalbagh Botanical Garden (tiles render once the Maps API key is
restricted to this app's package and SHA-1). The three map-type chips, zoom
and re-center FABs and the profile strip are all live, themed in purple.

## 6. Test cases

### TC1 — Default launch, Normal map

**Steps:** Launch the app.
**Expected:** Toolbar shows the student's USN + name, the "Normal" chip is
the active pill (filled purple), the map card renders at the pinned
location, and the profile strip at the bottom shows "USN · 25MCAR0139 ·
Yashika Chaudhary".

![TC1 — Normal map, profile visible](screenshots/25MCAR0139_tc1_normal.png)

> This screenshot also serves as the **USN + name** test case — the identity
> is visible both in the top app bar and in the bottom strip.

### TC2 — Switch to Satellite

**Steps:** Tap the **Satellite** chip.
**Expected:** The pill style flips — "Satellite" becomes the filled-purple
active pill and "Normal" returns to the muted idle style. `GoogleMap.mapType`
is set to `MAP_TYPE_SATELLITE`.

![TC2 — Satellite chip active](screenshots/25MCAR0139_tc2_satellite.png)

### TC3 — Switch to Hybrid and zoom in

**Steps:** Tap the **Hybrid** chip, then tap the **+** FAB twice.
**Expected:** "Hybrid" is now the active pill, the map type switches to
`MAP_TYPE_HYBRID`, and the camera animates to a tighter zoom level while
staying centered on the pinned location.

![TC3 — Hybrid map after zoom in](screenshots/25MCAR0139_tc3_hybrid_zoomed.png)

## 7. How to reproduce

1. Paste a Google Maps SDK key into `local.properties`:
   `MAPS_API_KEY=YOUR_KEY_HERE`
2. In GCP Console, restrict the key to the Android package
   `com.example.experiment11` + this machine's debug SHA-1.
3. Open `StudentProfile.kt` and set `val ACTIVE: StudentProfile = YASHIKA`.
4. From the project root:
   `./gradlew assembleDebug && adb install -r app/build/outputs/apk/debug/app-debug.apk`
5. Launch "Experiment11" from the device launcher.
