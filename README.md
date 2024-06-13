# Godot Engine Minimal Web Build

This setup configures a minimal web build targeting specifically web GUI use. It provides a most optimal setup for the purpose of making websites using Godot (WebGL), instead of HTML technologies. This strips everything not relevant to 2D GUI.

## Overview

The major bottlenecks for using Godot for pure (traditional) websites is size (thus impact loading speed) and adaptive GUI (e.g. on mobile platforms). The default official Godot build exports a web application around 40Mb in size.

https://www.google.com/ is around 1.0 MB transferred, 2.8 MB resources, Finish: 1.0 min, DOMContentLoaded: 210 ms, Load: 499 ms, with majority of resources/request finish within 200ms. https://Google.ca/maps contains 333 requests, 4.3 MB transferred, 9.7 MB resources, Finish: 12.82 s, DOMContentLoaded: 310 ms, Load: 603 ms. Google Doc is 278 requests, 5.6 MB transferre, 23.7 MB resources, Finish: 12.53 s, DOMContentLoaded: 514 ms, Load: 2.14 s.

In general, website size < 5Mb and loading (including resource decompression) within 3s is acceptable and considered fast.

## Setup (Update from Upstream)

To update from upstream (pull latest features), do ...

(Might want to keep this README).

## TODO

- [ ] Make web build template
- [ ] Make web build editor
- [ ] Provide scripts for generate required editor and export template files
- [ ] Demonstrate minimal web build size

## References

PENDING.

Official build optimization guide:

* https://docs.godotengine.org/en/stable/contributing/development/compiling/optimizing_for_size.html

Build optimization discussion:

* https://forum.godotengine.org/t/how-do-i-reduce-the-size-of-my-web-builds/21013
* https://www.reddit.com/r/godot/comments/8b67lb/guide_how_to_compress_wasmpck_file_to_make_html5/
* https://www.reddit.com/r/godot/comments/a3t8t4/how_low_can_godot_go/

Can we go as low as <5Mb?
