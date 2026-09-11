# JMeter Performance Training

Performance testing project created with Apache JMeter using the ZigWheels website.

This project demonstrates:

- HTTP request testing
- CSV parameterisation
- Regular Expression Extractors
- HTTP(S) traffic recording
- Response time monitoring
- Throughput and error-rate analysis
- JTL result generation
- HTML performance reporting

---

## Project Structure

```text
JMeterPerformanceTraining/
│
├── Recording/
│   └── Webpage Recording.jmx
│
├── ZigWheels/
│   ├── ZigWheels Performance Test.jmx
│   ├── bikes_locations.csv
│   └── results.jtl
│
├── Reports/
│   └── ZigWheels/
│       └── index.html
│
└── README.md
```

---

## Main Test Plan

Open:

```text
ZigWheels/ZigWheels Performance Test.jmx
```

### Search New Bikes

Uses CSV values to send requests to ZigWheels.

Variables:

```text
${location}
${bike_type}
```

Example:

```text
/new-bikes/search?location=Delhi&bike_type=sports
```

### Upcoming Bikes

Requests the ZigWheels Upcoming Bikes page.

Regular Expression Extractors retrieve:

```text
Bike Name
Bike Price
Expected Launch Date
```

Example extracted values:

```text
Honda CB 500
Rs. 2.80 Lakh
Sep 2026
```

---

## CSV Data

CSV file:

```text
ZigWheels/bikes_locations.csv
```

Example data:

```text
Delhi,sports
Mumbai,cruiser
Bangalore,adventure
Chennai,scooter
```

The values are loaded into:

```text
${location}
${bike_type}
```

This avoids hard-coding test data inside the HTTP request.

---

## HTTP(S) Test Script Recorder

The test plan includes an HTTP(S) Test Script Recorder.

Recorder port:

```text
8888
```

Firefox proxy settings used for recording:

```text
HTTP Proxy: 127.0.0.1
Port: 8888
```

Recorded browser requests are stored under:

```text
Recorded ZigWheels Journey
```

The recorded journey is disabled during normal performance execution so extra browser traffic does not affect the performance test.

---

## Performance Listeners

### View Results Tree

Shows detailed request and response information.

Useful for debugging.

### View Results in Table

Shows individual request results including:

```text
Sample Time
Status
Bytes
Latency
Connect Time
```

### Summary Report

Shows:

```text
Average Response Time
Minimum Response Time
Maximum Response Time
Error %
Throughput
```

### Aggregate Report

Shows additional statistics including:

```text
Average
Median
90th Percentile
95th Percentile
99th Percentile
Error %
Throughput
```

### Response Time Graph

Displays response times visually over time.

Graph interval:

```text
1000 ms
```

---

## Thread Group

The Thread Group uses JMeter properties:

```text
Threads: ${__P(threads,50)}
Ramp-up: ${__P(rampup,10)}
Loops:   ${__P(loops,5)}
```

Default training configuration:

```text
50 users
10 second ramp-up
5 loops
```

These values can be overridden from the command line.

---

## Run in JMeter GUI

Open:

```text
ZigWheels/ZigWheels Performance Test.jmx
```

For a small local test, use:

```text
Users: 1
Ramp-up: 1
Loops: 5
```

Then click the green **Start** button.

> ZigWheels is a live third-party website. Keep test loads low unless performance testing has been explicitly authorised.

---

## Run in Non-GUI Mode

From Git Bash, run JMeter through PowerShell:

```bash
powershell.exe -NoProfile -Command "& 'C:\Users\450 G10\Downloads\apache-jmeter-5.6.3\apache-jmeter-5.6.3\bin\jmeter.bat' -n -t 'C:\Users\450 G10\Desktop\training\JMETER\JMeterPerformanceTraining\ZigWheels\ZigWheels Performance Test.jmx' -Jthreads=1 -Jrampup=1 -Jloops=5 -l 'C:\Users\450 G10\Desktop\training\JMETER\JMeterPerformanceTraining\ZigWheels\results.jtl' -e -o 'C:\Users\450 G10\Desktop\training\JMETER\JMeterPerformanceTraining\Reports\ZigWheels'"
```

### Command Options

```text
-n           Run JMeter without the GUI
-t           Test plan to run
-Jthreads    Number of virtual users
-Jrampup     Ramp-up period
-Jloops      Number of loops
-l           Save results to a JTL file
-e           Generate HTML report
-o           HTML report output directory
```

---

## Generate a Fresh HTML Report

Remove the previous report and JTL file:

```bash
rm -rf "Reports/ZigWheels"
rm -f "ZigWheels/results.jtl"
```

Then run the non-GUI command again.

---

## Open the HTML Dashboard

The generated dashboard is located at:

```text
Reports/ZigWheels/index.html
```

Open it from Git Bash:

```bash
explorer.exe "Reports/ZigWheels/index.html"
```

The dashboard includes:

```text
Response Times
Throughput
Errors
Percentiles
APDEX
Request Success / Failure
Network Activity
```

---

## Example Test Result

A low-load run produced:

```text
10 HTTP samples
0 errors
0.00% error rate
Average response time: 643 ms
Minimum response time: 170 ms
Maximum response time: 1795 ms
Throughput: approximately 1.5 requests/second
```

---

## Tools

```text
Apache JMeter 5.6.3
Firefox
Git
GitHub
```

---

## Purpose

This project was created as part of performance testing training to practise:

- Creating JMeter test plans
- Configuring virtual users
- Parameterising requests with CSV data
- Extracting response data
- Recording browser HTTP/HTTPS traffic
- Measuring response time
- Measuring throughput
- Monitoring error rates
- Analysing percentiles
- Running JMeter in non-GUI mode
- Generating JTL results
- Generating HTML performance dashboards
