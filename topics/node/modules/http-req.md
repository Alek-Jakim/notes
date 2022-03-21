```javascript
// const https = require("https");
// const http = require("http");

const { request, get } = require("https");

const req1 = request("https://www.google.com", (res) => {
    res.on("data", (chunk) => {
        console.log(`Data chunk: ${chunk}`);
    });

    res.on("end", () => {
        console.log("No more data");
    })
});
req1.end();


// No need to call end function with get
get("https://www.google.com", (res) => {
    res.on("data", (chunk) => {
        console.log(`Data chunk: ${chunk}`);
    });

    res.on("end", () => {
        console.log("No more data");
    })
});





// const req2 = http.request("http://www.google.com", (res) => {
//     res.on("data", (chunk) => {
//         console.log(`Data chunk: ${chunk}`);
//     });

//     res.on("end", () => {
//         console.log("No more data");
//     })
// });

// this has to be called with http.request/https.request


//req2.end();
```