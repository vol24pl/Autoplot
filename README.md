# Autoplot

## Problem
Most people who plot Chia in parellel, are trying to optimise ploting with hardcoded delay between plots. For a regular setup, plotting in phase one is taking 2 cores, but after that it only takes one. So when creating a multiple parallel plots, trying to find a perfect delay can be mundane, and bad calculations can lead to CPU overuse (starting more plots than CPU can handle) or CPU underuse (having free unused cores that could be usefull for plotting).

**This is far from the optimal approach!**


## Solution

**Autoplot to the rescue!**

Thanks to the log files we know which plot is in which phase, so why not just use that knowledge? 

Autoplot is watching the logs in real time in order to count how many cores are used right now, and automatically start plotting, once we have 2 unused cores.

## How does it work?
This script does the following:
* Make a list of all log files in the log folder
* Count 0 cores as used
* For all log files do the the following:
    * Count +2 cores as used (so 2 are used for this logfile)
    * If logfile contains info about phase 1 finished, count -1 core (so 1 is used for this logfile)
    * If logfile contains info about phase 4 finished, count -1 core less (so 0 is used for this logfile)
* Check if declared total core count is greater then used cores count by two or more
   * if so create a new plot and repeat the whole process
   * if not, start everything from the top

## Installation and usage

1. Make sure you have the newest Python 3 (updated if needed): `$ python --version`
2. Download script: `$ git clone https://github.com/vol24pl/Autoplot.git`
3. Open script folder: `$ cd ./Autoplot/`
4. Adjust global variables `$ nano automatic-plotter.py`
5. Run script: `$ python automatic-plotter.py`


## Supported operating systems
This script works for **Linux** and **MacOS**, but making it work for Windows should be an easy task for any tech-savvy chia enthusiast. Feel free to fork and create a pull request :)
