# Electron buildpack

This downloads the linux x64 binary of electron and places it in `/app/vendor/electron`.

# This is only tested on the cedar-14 stack and may not work with the latest stack.

### Prerequisites

Your `.buildpacks` will need the following: 

```
https://github.com/ddollar/heroku-buildpack-apt.git
https://github.com/captain401/heroku-buildpack-xvfb.git
https://github.com/benschwarz/heroku-electron-buildpack.git
https://github.com/heroku/heroku-buildpack-nodejs.git
```

* Specifically, you want 'captain401/xvfb' because it creates the correct links for Xvfb. Otherwise it'll crash `/app/.apt/`

Your `Aptfile` should look like this: 

```
xvfb
x11-xkb-utils
xfonts-100dpi
xfonts-75dpi
xfonts-scalable
xfonts-cyrillic
libxfont1
libnotify4
```

Your `Procfile` will need to be run with `xvfb-run`. Here's an example of mine:

`web: DEBUG=* xvfb-run --server-args="-screen 0 1280x1028x24 -ac +extension GLX +render" node server.js`
