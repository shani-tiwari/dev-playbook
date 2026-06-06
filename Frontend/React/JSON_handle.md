 * .parse() (we need whole json data to start parsing)
 - loading indicator
 - is a synchronous task, so until parsing isn't done, the next line will not execute. and for that time period UI is blocked.
 - is a CPU intensive task.

- Solution:
    1. use worker thread if data is very large
    2. render only the visible data - virtulization - only create DOM node for visible data (u loose searching feature in this)
   # 3. NDJSON 
     - stream parsing  -  one valid JSON line at a time 
```js
// main thread
const blob = new Blob(
  [
    `
      onmessage = function(event) {
        const parsedData = JSON.parse(event.data);
        postMessage(parsedData);
      }
    `,
  ],
  { type: "application/javascript" }
);

const worker = new Worker(URL.createObjectURL(blob));
worker.onmessage = (event) => {
    setData(event.data);    // kya kaam hua
}

worker.postMessage(apiResponse);  // kya kaam karna hai

// how worker take work
self.onmessage = (event) => {
    const parsedData = JSON.parse(event.data);
    self. postMessage(parsedData);  // kya kaam hua
}