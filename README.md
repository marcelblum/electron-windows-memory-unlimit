Binaries of Electron using a fork of Chromium that sets the memory usage limit on Windows equal to that on macOS & Linux (16GB) instead of 8GB. Note: 8GB can only be exceeded on Windows if `sandbox` is off in the renderer (or `nodeIntegration` is on which automatically sets `sandbox` off).

Built using **Electron** v21.0.0-nightly.20220801, **Chromium** v105.0.5187.0, **Node** v16.16.0, **v8** v10.5.196-electron.0

re: https://github.com/electron/electron/issues/31330, https://github.com/electron/electron/issues/35032
