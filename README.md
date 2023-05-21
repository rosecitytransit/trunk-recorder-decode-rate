Trunk Recorder decode rates logging plugin
==========================================

Uses [Trunk Recorder](https://github.com/robotastic/trunk-recorder)'s `trunk_message` plugin hook to log trunking system control channel decoding rates to decode_rates.csv in the captureDir as specified in config.json. Requires versions of Trunk Recorder on or after May 17, 2023 (commit 5c07ef0).

On each startup of Trunk Recorder, a header line of `timestamp,shortName,shortName` will be added to the file.

Includes a PHP script which outputs an SVG graph of the rates.

To use:
1. Make a directory named "decode_rates" within Trunk Recorder's plugins directory and either copy these files or clone the repository into that directory
2. Apply the patch as follows by running this command from your root trunk-recorder code directory (where the CMakeLists.txt file is):
```bash
patch -p1 < plugins/decode_rates/decode_rates.patch
```
3. Build the Trunk Recorder program normally
4. Add a `"frequency": 60` entry to the Global Configs section of your config.json, where `60` is the number of seconds between logging entries
5. Optionally put the PHP file somewhere Web accessible and edit it

OR
1. Build Trunk Recorder normally, and run `sudo make install` at the end to install it
2. Run `cmake ./`, `make` and then `sudo make install` in this directory to build and install the plugin
3. Add to your config.json:
```yaml
 "plugins": [
    {
        "name": "decode_rate",
        "library": "decode_rate.so",
        "frequency": 60
    }]
```
4. Optionally put the PHP file somewhere Web accessible and edit it
