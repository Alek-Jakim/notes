# Planets Project

### CSV Files

A Comma Separated Values (CSV) file is a plain text file that contains a list of data. These files are often used for exchanging data between different applications. For example, databases and contact managers often support CSV files.

A good npm package for parsing CSV files is:

```bash
npm install csv-parse
```


```javascript
import { parse } from "csv-parse";
import fs from "fs"

const log = console.log;

const isHabitablePlanet = (planet) => {
    return planet["koi_disposition"] === "CONFIRMED" && planet["koi_insol"] > 0.36 && planet["koi_insol"] < 1.11 && planet["koi_prad"] < 1.6;
}

const habitablePlanets = [];

fs.createReadStream("kepler_data.csv")
    .pipe(parse({
        comment: "#",
        columns: true
    }))
    .on("data", (data) => {
        // here we get an array of buffers - just objects that node uses to represent a collection of bytes
        if (isHabitablePlanet(data)) {
            habitablePlanets.push(data);
        }
    })
    .on("error", (error) => {
        log(error);
    })
    .on("end", () => {
        log(habitablePlanets.map((planet) => planet["kepler_name"]));
        log(`${habitablePlanets.length} habitable planets found!`);
    });

```