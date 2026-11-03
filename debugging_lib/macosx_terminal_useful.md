//robert coffman
//quick dump for context switching from linux/win to macosx ^_~

# some quick developer commands on a macosx 

## list servers/services 
detecting servers running

### detecting who is running servers,

```
lsof -nP -iTCP:8090 -sTCP:LISTEN
```

### list all servers running based on programming languages

```
lsof -nP -iTCP -sTCP:LISTEN | grep -iE "dart|python|flutter" 
```

## Terminal Command to list all usb hub and connected devices 

For a more readable version with names, speeds and power use:


```
system_profiler SPUSBDataType
```
On newer macOS versions this may print nothing. Then use this instead:

```
system_profiler SPUSBHostDataType
```
The same information is in System Information, under USB in the sidebar.


### additional info:

system_profiler SPUSBDataType already lists nested devices. Anything plugged into a hub appears indented under that hub's entry. Nothing shows under your hubs only because macOS hasn't detected the MPK Mini yet. When it's working, the output looks like this:


        USB2.1 Hub:
          ...
            MPK mini 3:
              Product ID: ...
              Manufacturer: Akai
The full output is long, so it's easy to lose track of what is nested under what. These options make the nesting clearer.

The device tree, names only. This is the command from before:


ioreg -p IOUSB -w0 | sed 's/<class.*//'
system_profiler as a tree, with manufacturers. It reads system_profiler's JSON output and prints one indented line per device:


system_profiler SPUSBDataType -json 2>/dev/null | python3 -c '
import json, sys
def walk(items, depth):
    for i in items:
        print("  " * depth + i.get("_name", "?") + ("  [" + i["manufacturer"] + "]" if "manufacturer" in i else ""))
        walk(i.get("_items", []), depth + 1)
walk(json.load(sys.stdin)["SPUSBDataType"], 0)'
On your Mac right now it prints:


USB31Bus
USB31Bus
  USB3.1 Hub  [GenesysLogic]
  USB2.1 Hub  [GenesysLogic]
USB31Bus
Each USB31Bus is one of the Mac's own USB controllers. Devices on a hub would appear one level further in, under the hub.

Only the lines you need from the full report:

```
system_profiler SPUSBDataType 2>/dev/null | grep -E "^ +[^ ].*:$|Manufacturer|Location ID"

```
This keeps device names, manufacturers and location IDs. The location ID also shows nesting: a device on the hub at 0x01100000 gets an ID starting 0x011, such as 0x01110000.
