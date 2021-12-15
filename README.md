# IMPINJ RFID MongoDB Data Collector

## Configuration

### Environment

You will require Apache Ant, an up-to-date Java runtime environemt (JRE), and a local install of MongoDB server. You **must** start an instance of MongoDB server *before* running this tool.

### Tags

You must list all tags for which you wish to record data in ```examples/tags.txt```. The tool will create a record for each tag at every snapshot. An example of the tags file is as follow:

```
300833B2DDD9014011110001
300833B2DDD9014011110002
300833B2DDD9014011110003
...
```

Optionally, if you wish to restrict recording for specific tags to one or two antennas, you may specify which tags as follows:

```
300833B2DDD9014011110001:1:2 // restricts to antenna 1 and 2
...
```

### Rate

By default, the data collector will save a snapshot of tag states every second and will run for a maximum of 3600 seconds (1 hour). You can customise these values by editing the following variables in ```examples/source/org/impinj/llrp/ltk/examples/datacollector/DataCollector.java```:

```
static int numSnapshots = 3600;
static int sleepTime = 1000;
```

## Usage

To run this code you must change directory into the `example` sub-directory of the root module folder.

To start the module, use the following command, replacing 'IP_ADDRESS' with the IP of your Speedway Revolution reader.

> ant -Dreadername=<IP_ADDRESS> run-datacollector

For example, if your Speedway Revolution reader has an IP address of 192.168.1.3, you would use the following command:

> ant -Dreadername=192.168.1.3 run-datacollector

The module will load and after a few seconds will request that you provide a label for the recording session, which will be used to label the collection that will be inserted into the MongoDB database.

## Acknowledgement

Based on the LLRP Toolkit (LTK) from Impinj, available [here](https://support.impinj.com/hc/en-us/articles/202756168-Hello-LLRP-Low-Level-Reader-Protocol-), with additional code to generate periodic snapshots of tag data and post them to a MongoDB server.
