# v-cargens

Car generator information from GTA V which you can use as vehicle spawn locations in alternative multiplayer mods, currently providing **9947** coordinates.

## NoZoneVehicles Version

This JSON file contains car generator coordinates and models Rockstar specified in YMAP files. Only **1084** coordinates have pre-defined vehicle models, you can either keep them or ignore them and spawn your own vehicles.

## ZoneVehicles Version

In addition to NoZoneVehicles data, this JSON file has vehicle models that have a chance to spawn at the coordinates. In this version **9905** coordinates have pre-defined vehicle models. (Generated from popcycle.dat)

## Example Car Generator

```json
{
  "x": -1595.1792,
  "y": -3170.36426,
  "z": 12.854578,
  "heading": -208.770676,
  "models": [
    "airbus",
    "rentalbus"
  ]
}
```

## Usage (RAGEMP JS)

```js
const data = require("./CarGens_ZoneVehicles");

let count = 0;
for (let i = 0; i < data.length; i++) {
    if (data[i].models.length === 0) {
        continue;
    }

    // No checks for boats etc. - might cause weird spawns
    mp.vehicles.new(data[i].models[ Math.floor(Math.random() * data[i].models.length) ], new mp.Vector3(data[i].x, data[i].y, data[i].z), {
        heading: data[i].heading
    });

    count++;
}

console.log(`Created ${count} vehicles.`);
```

## Notes

- Even though there are 9000+ coordinates available, it doesn't mean you should spawn vehicles on all coordinates. Personally, using 20-30% of the locations is more than enough.

- ZoneVehicles version didn't had any checks while generating, so car generators at land (like a car park) might have a boat as one of the vehicle models. This might change in the future but no promises.

- Some vehicles might spawn in air, in that case try using SET_VEHICLE_ON_GROUND_PROPERLY native.
