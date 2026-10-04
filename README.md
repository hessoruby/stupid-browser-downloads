# Stupid Browser downloads

A stupidly simple desktop browser. It opens websites. That's basically the point.

This repository hosts release files and notices. Browser source and personal browser data are not published here.

## Download

Open [the download page](https://www.hessoruby.in/stupid-browser) or [Releases](https://github.com/hessoruby/stupid-browser-downloads/releases).

The 0.1.1 release is a testing preview for Linux x86_64 and Windows x64. Linux runtime checks use disposable profiles. Windows files are cross-built on Linux and have not been validated on a native Windows system. Builds are unsigned; a signed automatic update channel is not implemented.

Linux: download the AppImage, then run:

```bash
chmod +x Stupid-Browser-0.1.1-x86_64.AppImage
./Stupid-Browser-0.1.1-x86_64.AppImage
```

If FUSE is unavailable, extract the AppImage and run it:

```bash
./Stupid-Browser-0.1.1-x86_64.AppImage --appimage-extract
./squashfs-root/AppRun
```

The Linux tar.gz contains the unpacked application. Extract it into a writable application directory and run `stupid-browser` as an ordinary user. Never disable Chromium's sandbox to run it.

Windows: close the old browser, download and extract the portable ZIP into a new folder, then run `stupid-browser.exe`. Browser profiles remain in the existing user-data directory. For example, in PowerShell:

```powershell
Expand-Archive .\Stupid-Browser-0.1.1-x64.zip -DestinationPath .\stupid-browser
.\stupid-browser\stupid-browser.exe
```

Windows may warn about the unsigned executable. Native Windows execution is not yet validated. The graphical installer is not included because its Wine build helper failed; the incomplete helper is not distributed.

## Verify files

Each release supplies `SHA256SUMS.txt` and `BUILD_INFO.json`. With downloaded files and checksums in the same directory:

```bash
sha256sum --ignore-missing -c SHA256SUMS.txt
```

On Windows PowerShell:

```powershell
Get-FileHash .\Stupid-Browser-0.1.1-x64.zip -Algorithm SHA256
```

Compare the result with `SHA256SUMS.txt`. Checksums detect corruption; they are not a substitute for signed release verification. Distribution currently relies on HTTPS and this GitHub account.

## Scope and limitations

The browser uses Electron's Chromium engine, sandboxed website tabs and separate normal/private/Temp sessions. It includes history, downloads, profiles, tab sleeping, current-tab video recording and a native ad/tracker blocker. It does not guarantee that every advertisement can be blocked or every site's videos can be downloaded.

Current-tab recording uses Chromium’s built-in encoder when FFmpeg is absent. On Windows x64, open the video download panel and click UPDATE HELPER once to install checksum-verified portable yt-dlp, Node.js and FFmpeg. Python and administrator access are not required; setup downloads about 190 MB and needs an internet connection. Linux/macOS helper setup requires Python, Node.js and FFmpeg. Native helper binaries are downloaded only on your request and are not bundled in the browser archive. Protected DRM playback, a website-password vault, full Chrome extension compatibility, encrypted sync and a signed updater are not implemented.

Report download problems through this repository's issues. Do not attach passwords, cookies, personal browser profiles or private browsing data.

## Licenses

Stupid Browser uses the MIT license in [LICENSE](LICENSE). Bundled dependencies have their own licenses and source references in [THIRD_PARTY_NOTICE.txt](THIRD_PARTY_NOTICE.txt) and [THIRD_PARTY_LICENSES.txt](THIRD_PARTY_LICENSES.txt). Electron and Chromium license notices are also included in the application distributions. Proprietary Chrome components and Widevine binaries are not included.
