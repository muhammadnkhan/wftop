# Wavefront Top (wftop) [![Build Status](https://travis-ci.org/wavefrontHQ/wftop.svg?branch=master)](https://travis-ci.org/wavefrontHQ/wftop)

[Wavefront](https://docs.wavefront.com/) is a high-performance streaming analytics platform for monitoring and optimizing your environment and applications.

Wavefront Top (wftop) is an interactive tool for exploring the live metric ingestion data shape and to explore which metric namespaces were used in the last X days. Lag information (from wallclock of the machine running wftop compared to the ignested timestamp) is also available which can be used to discover data points that might be lagging behind (likely at the source).

## Features
  * Slice real-time metrics, host names, point tag keys, point tags into namespaces ("folders")
  * Compute per namespace "pps" (for point tags, counting each occurrence)
  * Compute per namespace "% Accessed" (in the last X days, configurable)
  * Compute median, p75 and p99 lag for timestamps of each namespace (compared to wall-clock of the machine running wftop)
  * Drill-down into each namespace via selection
  * Customizable separators (defaults to ".", "-", "_")
  * Multiple sort dimensions
  * Start/Stop support
  * Automatic reconnection on server disconnects or network faults
  * Console emulation (--emulator) for high-resolution rendering
  * Credentials storage on "user.home" location for fast start-up (also supports --token and --cluster arguments)

## Screenshots

Setting up wftop (the tool will persist the cluster/token to ~/.wftop)

![Setup Screen](https://raw.githubusercontent.com/wavefronthq/wftop/master/screenshots/SetupScreen.png)

UI to browse top-level metric namespaces (delimiters are configurable and can be changed in the "Config" screen). Est. PPS estimates the pps sent by a particular namespace and % Accessed indicates how many of those points are found to be access in the last X days (configuration in "Config" screen between 1 and 60). Lag information is also shown which shows the median, p75 and p99 lag of metrics for each namespace.

![Setup Screen](https://raw.githubusercontent.com/wavefronthq/wftop/master/screenshots/BrowseScreen.png)

Selecting a "folder" allows the user to drilldown into a single metric namespace.

![Setup Screen](https://raw.githubusercontent.com/wavefronthq/wftop/master/screenshots/DrillDown.png)

Configuration screen to control sample rate (typical Wavefront clusters allow up to 5% sampling, wftop will automatically scale all pps measurements based on this number and backend data distribution topologies). Separators (each) control how metrics are split up into "folders". Usage lookback (days) control when a metric is considered "used" (a value of 7 means the metric would be considered used if it was accessed in any of the last 7 days).

![Setup Screen](https://raw.githubusercontent.com/wavefronthq/wftop/master/screenshots/ConfigurationScreen.png)

## Requirements
  * Java >= 1.8
  * maven (to compile)
  * Any Wavefront cluster >= 2019-18.8
    * Older Wavefront clusters will still work with wftop but pps and % Accessed information will not be accurate/available.

## Overview
  * Simply run mvn clean install to compile the tool
  * ./target/wftop is all you need to do afterwards
  
## To start developing

```
$ git clone github.com/wavefronthq/wftop ${directory}
$ cd ${directory}
$ mvn clean install
```

## Contributing
Public contributions are always welcome. Please feel free to report issues or submit pull requests.