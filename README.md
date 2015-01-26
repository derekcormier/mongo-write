# mongo-write
Write to MongoDB from the terminal

## Terminal Usage
mongowrite is a simple python script that can be run from the terminal. Here are a few examples of how to use it from the terminal.

If you would like to write to localhost with the default port (27017):
```bash
mongowrite -db mydb -coll mycollection key,value key,value
```

If you would like to write to a different database or port
```bash
mongowrite -host 192.168.0.1 -port 12345 -db mydb -coll mycollection key,value key,value
```

## Arduino Yún Usage
I created this script specifically so that I could easily write to MongoDb from an arduino Arduino Yún using the Process library. Here's an example Sketch that uses mongowrite:
```C
#include <Process.h>

void setup() {
  // Initialize the Bridge
  Bridge.begin();
  
  // Kick off the process
  Process p;
  p.begin("mongowrite");
  // Specify the host
  p.addParameter("-host");
  p.addParameter("192.168.0.1");  
  // Specify the database
  p.addParameter("-db");
  p.addParameter("mydb");
  // Specify the collection
  p.addParameter("-coll");
  p.addParameter("mycollection");
  // Add the data
  p.addParameter("key,value");
  p.addParameter("key2,value2");
  p.run();
}

void loop() {
  // Nothing here this time
}
```

## Installation
You will need to install the python-openssl and pymongo Python modules.

After this, just copy the script to your disk. If you plan to call if from anywhere or as a Process on your Yún, make sure it's in your PATH.