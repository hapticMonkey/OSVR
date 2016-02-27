# OSVR

OSVR Does not install properly on Yosemite under Homebrew.

I performed the following to get OSVR and the OSVR Viewer installed under Yosemite on a Mac Mini.

From the Apple menu choose Go->Utilities->Terminal

Type (or copy/paste) the following in the terminal, (It will ask you for your admin password): 

/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

If you follow the instructions from the OSVR Installation Instructions it tells you to install OSVR from Homebrew but it will fail with the following error:
<hr>
<code>

bash-3.2$ brew install osvr-core --HEAD
==> Installing osvr-core from osvr/osvr
Error: No available formula with the name "opencv" (dependency of osvr/osvr/osvr-core)
==> Searching for similarly named formulae...
Error: No similarly named formulae found.
==> Searching taps...
These formulae were found in taps:
homebrew/science/opencv                  homebrew/science/opencv3               
To install one of them, run (for example):
  brew install homebrew/science/opencv

</code>
<hr>
The reason is that the location of the opencv has moved.  We need to install it first before installing OSVR.  Do not install opencv3.  OSVR requires opencv2. Perform the install in this order (be prepared to wait a very long time as each dependancy is downloaded and installed):

brew tap homebrew/science
brew install opencv

brew tap OSVR/osvr
brew install osvr-core --HEAD

It is now installed.  You can ignore the compiler warnings.

You will need to locate the default osvr_server_config.json file and overwrite it in the default location.  If you need to make any custome changes to the file this where you should put it.

/usr/local/Cellar/osvr-core/HEAD/share/osvrcore/osvr_server_config.json

To run OSVR:

/usr/local/Cellar/osvr-core/HEAD/bin/osvr_server /usr/local/Cellar/osvr-core/HEAD/share/osvrcore/osvr_server_config.json


Installing osvr_viewer

The OSVR-Tracker-Viewer installer for Homebrew does not work because the code for open-scene-graph is upstream incompatible.  To install OSVR-Tracker-Viewer you have to run a separate install for open-scene-graph and then this Homebrew installer.

Steps: From the terminal run the following

brew install https://raw.github.com/domoritz/homebrew/master/Library/Formula/open-scene-graph.rb -v

brew install --HEAD https://raw.githubusercontent.com/hapticMonkey/OSVR/master/osvr-tracker-viewer.rb -v

It is now installed, again ignore the compiler warnings.

To run the OSVR Tracker Viewer:

/usr/local/Cellar/osvr-tracker-viewer/HEAD/OSVRTrackerView
