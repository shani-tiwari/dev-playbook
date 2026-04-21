# NodeJS Tools and Packages

## Load Testing
- **autocannon**: Sends multiple requests to check the load on a server.

## Logging & Monitoring
- **morgan**: Tells which route is called and how much time it took to respond.
  - Usage: `app.use(morgan("dev"));`
  - Formats:
    - `morgan("dev")` - short format
    - `morgan("combined")` - long format
    - `morgan("tiny")` - shortest format

## Asynchronous Communication
- **amqplib**: Handle asynchronous communication (message queuing) between servers.
