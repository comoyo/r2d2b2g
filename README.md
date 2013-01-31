Remote debugging (Comoyo edition)
---------------------------------

r2d2b2g is an experimental prototype test environment for Firefox OS
in the form of a Firefox Desktop addon for
[Linux](https://ftp.mozilla.org/pub/mozilla.org/labs/r2d2b2g/r2d2b2g-linux.xpi),
[Mac](https://ftp.mozilla.org/pub/mozilla.org/labs/r2d2b2g/r2d2b2g-mac.xpi), and
[Windows (crashy)](https://ftp.mozilla.org/pub/mozilla.org/labs/r2d2b2g/r2d2b2g-windows.xpi).

This is the modified Comoyo addon for development. The main change is that it doesn't use gaia
as a submodule. The recommended way to have gaia there is to symlink it.

To hack on it, clone this repository, then:

    git submodule init
    git submodule update
    make build
    ln -s path_to_your_gaia_repo gaia
    make package

This process will download (only the first time) a particular copy of B2G. This can be
tweaked so that the latest B2G is always downloaded by commenting out the
`B2G_ID` in the Makefile. When it finishes, you will have a file named
`r2d2b2g.xpi` in the `./addon` folder that you can install as a exension in
your Firefox browser.

Remote debugging
----------------

In order to connect the debugger remotely to the simulator instance, you have
to set `devtools.debugger.remote-enabled` to `true` in your `about:config`.
After doing that you should have a `Connect...` menu item in your `Tools/Web
Developer` menu that you cna use to do remote debugging.

After starting the simulator, open the Error Console in Firefox (`Tools/Web
Developer/Error Console`) and look for the message `info: r2d2b2g: rsc.remoteDebuggerPort: found free port  xxxxx`,
where `xxxxx` is the port you have to point the remote debugger to in order to
connect to the running Simulator instance.

