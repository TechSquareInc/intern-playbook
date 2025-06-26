# Getting on Slack

## Installation

1. Go to the Slack [downloads page](https://slack.com/downloads/linux) and download the RPM file.
2. The slack rpm depends on `libappindicator-gtk3`. `libappindicator` relies on `epel-release rpm`. To install `epel-release rpm` run `sudo yum install epel-release rpm`. To install `libappindicator-gtk3` run `sudo yum install libappindicator-gtk3`.
3. Locate the Slack rpm file you just downloaded (likely in your Downloads directory) `cd Downloads` and run `yum install slack-<your-version>.rpm` to install. 
