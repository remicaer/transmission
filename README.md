> [!WARNING]
> **This is an unofficial, entirely vibecoded fork of Transmission.**
> Every change in it was written by an AI coding assistant (Claude), because Remi wanted a sequential download toggle in Transmission for her own use.
> It is not affiliated with or endorsed by the Transmission project, it has had no real review or testing beyond "it works on Remi's Mac", and it is not maintained.
> It's online only in case someone else finds it helpful. **Use it at your own risk.** For anything serious, use [official Transmission](https://transmissionbt.com/).

## What this fork adds

A **sequential download** toggle, so pieces download in order (handy for previewing a video while it's still downloading). Upstream Transmission already supports sequential download in its engine and RPC, but its GUIs have no switch for it ([transmission/transmission#6257](https://github.com/transmission/transmission/issues/6257)). This fork adds one to:

* **macOS app**
  * a **Download Sequentially** toolbar button (add it via right-click on the toolbar → *Customize Toolbar…*); the icon is crossed out when sequential download is off
  * a **Download sequentially** checkbox in Inspector → Options
  * a **Download Sequentially** item in the Transfers menu and the right-click menu
  * a **Download new transfers sequentially** setting in Preferences → Transfers → Adding, to make it the default for newly added torrents
* **Web UI**: a **Download sequentially** item in the right-click menu

The GTK and Qt apps are unchanged.

## Download (macOS)

Grab `Transmission-sequential-macOS.zip` from the [Releases page](https://github.com/remicaer/transmission/releases).

* The app is **not signed or notarized**, so macOS will block it the first time. Either right-click the app → **Open**, or go to System Settings → Privacy & Security → **Open Anyway**. If macOS says it is "damaged", run `xattr -dr com.apple.quarantine /path/to/Transmission.app`.
* It shares settings and the torrent list with official Transmission (same bundle ID). Don't run both at once.
* Automatic updates are disabled, so it never "updates" itself back to official Transmission. Check the Releases page for new builds.
* Translations are not included in the release build; the UI is English only.

## About

Transmission is a fast, easy, and free BitTorrent client. It comes in several flavors:
  * A native macOS GUI application
  * GTK+ and Qt GUI applications for Linux, BSD, etc.
  * A Qt-based Windows-compatible GUI application
  * A headless daemon for servers and routers
  * A web UI for remote controlling any of the above
  
Visit https://transmissionbt.com/ for more information.

## Documentation

[Transmission's documentation](docs/README.md) is currently out-of-date, but the team has recently begun a new project to update it and is looking for volunteers. If you're interested, please feel free to submit pull requests!

## Command line interface notes

Transmission is fully supported in transmission-remote, the preferred cli client.

Three standalone tools to examine, create, and edit .torrent files exist: transmission-show, transmission-create, and transmission-edit, respectively.

Prior to development of transmission-remote, the standalone client transmission-cli was created. Limited to a single torrent at a time, transmission-cli is deprecated and exists primarily to support older hardware dependent upon it. In almost all instances, transmission-remote should be used instead.

Different distributions may choose to package any or all of these tools in one or more separate packages.

## Building

Transmission has an Xcode project file (Transmission.xcodeproj) for building in Xcode.

For a more detailed description, and dependencies, visit [How to Build Transmission](docs/Building-Transmission.md) in docs

### Building a Transmission release from the command line

```bash
$ tar xf transmission-4.1.0.tar.xz
$ cd transmission-4.1.0
# Use -DCMAKE_BUILD_TYPE=RelWithDebInfo to build optimized binary with debug information. (preferred)
# Use -DCMAKE_BUILD_TYPE=Release to build full optimized binary.
$ cmake -B build -DCMAKE_BUILD_TYPE=RelWithDebInfo
$ cd build
$ cmake --build .
$ sudo cmake --install .
```

### Building Transmission from the nightly builds

Download a tarball from https://build.transmissionbt.com/job/trunk-linux/ and follow the steps from the previous section.

If you're new to building programs from source code, this is typically easier than building from Git.

### Building Transmission from Git (first time)

```bash
$ git clone --recurse-submodules https://github.com/transmission/transmission Transmission
$ cd Transmission
# Use -DCMAKE_BUILD_TYPE=RelWithDebInfo to build optimized binary with debug information. (preferred)
# Use -DCMAKE_BUILD_TYPE=Release to build full optimized binary.
$ cmake -B build -DCMAKE_BUILD_TYPE=RelWithDebInfo
$ cd build
$ cmake --build .
$ sudo cmake --install .
```

### Building Transmission from Git (updating)

```bash
$ cd Transmission/build
$ cmake --build . -t clean
$ git submodule foreach --recursive git clean -xfd
$ git pull --rebase --prune
$ git submodule update --init --recursive
$ cmake --build .
$ sudo cmake --install .
```

## Contributing

### Code Style

You would want to setup your editor to make use of the .clang-format file located in the root of this repository and the eslint/prettier rules in web/package.json.

If for some reason you are unwilling or unable to do so, there is a shell script which you can use: `./code_style.sh`

### Translations

See [language translations](docs/Translating.md).

## Sponsors

<table>
 <tbody>
  <tr>
   <td align="center"><img alt="[MacStadium]" src="https://uploads-ssl.webflow.com/5ac3c046c82724970fc60918/5c019d917bba312af7553b49_MacStadium-developerlogo.png" height="30"/></td>
   <td>macOS CI builds are running on a M1 Mac Mini provided by <a href="https://www.macstadium.com/company/opensource">MacStadium</a></td>
  </tr>
  <tr>
   <td align="center"><img alt="[SignPath]" src="https://avatars.githubusercontent.com/u/34448643" height="30"/></td>
   <td>Free code signing on Windows provided by <a href="https://signpath.io/?utm_source=foundation&utm_medium=github&utm_campaign=transmission">SignPath.io</a>, certificate by <a href="https://signpath.org/?utm_source=foundation&utm_medium=github&utm_campaign=transmission">SignPath Foundation</a></td>
  </tr>
 </tbody>
</table>
