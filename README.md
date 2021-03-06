# Telemetry

Telemetry is a super simple API for sending point metrics to [Influxdb](https://docs.influxdata.com/influxdb) in batches at a given time interval. It's just a simple wrapper for Influxdb's REST API. As points are created they're timestamped and cached on disk so you'll never lose a metric.

### Installation
```
npm install react-native-telemetry --save
```

### Usage
```
import Telemetry from 'react-native-telemetry';

// Configure Telemetry
Telemetry.config({
  influxUrl: 'http://10.0.0.162:8086/write?db=testdb',
  basicAuth: 'influx_username:password',
  sendInterval: 5, // Time window in seconds for batching events
  defaultTags: { defaultTag1: 'some_value' },
  log: (message) => console.log(message),
});

// Send a point
Telemetry.point(
  'example_measurement',
  { value1: 42, value2: true, value3: 'string'},
  { host: 'value1', cpu: 'value2' },
);

// Force all unsent points to be sent.
Telemetry.flush();
```
