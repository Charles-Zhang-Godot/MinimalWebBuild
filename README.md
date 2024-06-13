# Godot Engine Minimal Web Build

This setup configures a minimal web build targeting specifically web GUI use. It provides a most optimal setup for the purpose of making websites using Godot (WebGL), instead of HTML technologies. This strips everything not relevant to 2D GUI.

## Overview

The major bottlenecks for using Godot for pure (traditional) websites is size (thus impact loading speed) and adaptive GUI (e.g. on mobile platforms). The default official Godot build exports a web application around 40Mb in size.

https://www.google.com/ is around 1.0 MB transferred, 2.8 MB resources, Finish: 1.0 min, DOMContentLoaded: 210 ms, Load: 499 ms, with majority of resources/request finish within 200ms. https://Google.ca/maps contains 333 requests, 4.3 MB transferred, 9.7 MB resources, Finish: 12.82 s, DOMContentLoaded: 310 ms, Load: 603 ms. Google Doc is 278 requests, 5.6 MB transferre, 23.7 MB resources, Finish: 12.53 s, DOMContentLoaded: 514 ms, Load: 2.14 s.

In general, website size < 5Mb and loading (including resource decompression) within 3s is acceptable and considered fast.

## Setup (Update from Upstream)

To update from upstream (pull latest features), do ...

(Might want to keep this README).

## Stats

Notice most of earlier build stats are from `master` branch which is simply not what we should be using (we were expecting `4.2`). In general, making a custom build through configuration changes is quite straightforward, while every time we change target it requires rebuilding everything, it's fairly fast for v4.2.

|Build Config/Measure|Config|Build Size|Build Time|Comment|
|-|-|-|-|-|
|Win32 x64 Editor|`scons`|120Mb|7min38s||
|Win32 x32 Export Template|`scons platform=windows target=template_release arch=x86_32`|52Mb|5min49s||
|Win32 x64 Optimized Export Template|` scons platform=windows target=template_release arch=x86_64 lto=full optimize=size module_text_server_adv_enabled=no module_text_server_fb_enabled=yes module_basis_universal_enabled=no module_bmp_enabled=no module_camera_enabled=no module_csg_enabled=no module_dds_enabled=no module_enet_enabled=no module_gridmap_enabled=no module_hdr_enabled=no module_jsonrpc_enabled=no module_ktx_enabled=no module_mbedtls_enabled=no module_meshoptimizer_enabled=no module_minimp3_enabled=no module_mobile_vr_enabled=no module_msdfgen_enabled=no module_multiplayer_enabled=no module_noise_enabled=no module_navigation_enabled=no module_ogg_enabled=no module_openxr_enabled=no module_raycast_enabled=no module_regex_enabled=no module_squish_enabled=no module_svg_enabled=no module_tga_enabled=no module_theora_enabled=no module_tinyexr_enabled=no module_upnp_enabled=no module_vhacd_enabled=no module_vorbis_enabled=no module_webrtc_enabled=no module_websocket_enabled=no module_webxr_enabled=no module_zip_enabled=no`|45.86Mb|9min22s||
|Minimal Web Export Template|`scons platform=web target=template_release`|45Mb|3min27s||
|Minimal Web Export Template Optimized|`scons platform=web target=template_release optimize=size module_text_server_adv_enabled=no module_text_server_fb_enabled=yes module_basis_universal_enabled=no module_bmp_enabled=no module_camera_enabled=no module_csg_enabled=no module_dds_enabled=no module_enet_enabled=no module_gridmap_enabled=no module_hdr_enabled=no module_jsonrpc_enabled=no module_ktx_enabled=no module_mbedtls_enabled=no module_meshoptimizer_enabled=no module_minimp3_enabled=no module_mobile_vr_enabled=no module_msdfgen_enabled=no module_multiplayer_enabled=no module_noise_enabled=no module_navigation_enabled=no module_ogg_enabled=no module_openxr_enabled=no module_raycast_enabled=no module_regex_enabled=no module_squish_enabled=no module_svg_enabled=no module_tga_enabled=no module_theora_enabled=no module_tinyexr_enabled=no module_upnp_enabled=no module_vhacd_enabled=no module_vorbis_enabled=no module_webrtc_enabled=no module_websocket_enabled=no module_webxr_enabled=no module_zip_enabled=no disable_advanced_gui=yes disable_3d=yes`|25.63Mb|2min|Notice we had `disable_advanced_gui=yes disable_3d=yes`; Do `$env:PATH = "$env:PATH;C:\Applications\emsdk\upstream\emscripten"` otherwise `web` platform will be marked as invalid|
|Minimal Web Editor|PENDING||||
|Win64 Editor v4.2 Build|(4.2)`scons`|101Mb|5min28s|

(We might still be able to disable audio engine and physics engine)

Notice we can still use the official editor for editing scenes even when using custom export templates (that may or may not have all supported engine features).

## TODO

- [ ] Figure out how to install Emscripten
    * Hard to compile from source
    * Same error with `choco install emscripten` (Per https://emscripten.org/docs/getting_started/downloads.html)
- [ ] Make web build template
- [ ] Make web build editor
- [ ] Provide scripts for generate required editor and export template files
- [ ] Demonstrate minimal web build size

## Troubleshooting

Notice we should NOT use `master` branch for web builds per https://github.com/godotengine/godot/issues/56932.

## References

Build guides:

* https://docs.godotengine.org/en/stable/contributing/development/compiling/compiling_for_windows.html: Including basic build and export template build.
* https://docs.godotengine.org/en/stable/contributing/development/compiling/compiling_for_web.html

Official build optimization guide:

* https://docs.godotengine.org/en/stable/contributing/development/compiling/optimizing_for_size.html

Build optimization discussion:

* https://forum.godotengine.org/t/how-do-i-reduce-the-size-of-my-web-builds/21013
* https://www.reddit.com/r/godot/comments/8b67lb/guide_how_to_compress_wasmpck_file_to_make_html5/
* https://www.reddit.com/r/godot/comments/a3t8t4/how_low_can_godot_go/

Can we go as low as <5Mb?
