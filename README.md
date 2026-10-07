# qs-kit

What the Quickshell apps in `~/Code` (Omvision, Omvida) share, so a fix made for one is made for
both.

- `bin/qs-check`: the checks a change must pass (qmllint against a baseline, the no-pixel-numbers
  rule, an offscreen load, the app's tests). Each app's `bin/check` execs it with its own root;
  the app's `.qs-kit` file names the app, its steps, the directories to skip and how to start it
  offscreen for the load step, and may add steps of its own (Omvida's `bar`). The script's header
  lists the details.

## Why only scripts

Quickshell loads QML only from inside an app's own config folder: an import of `../qs-kit/qml`
fails at startup with "Module path … is outside of the config folder", though `qmltestrunner`
accepts it. So shared QML components (a kinetic-scrolling Flickable, a test harness) can't live
here; each app keeps its own copy, with a comment naming where it came from.

## Checking a change here

Run both apps' checks: `~/Code/omvision/bin/check` and `~/Code/omvida/bin/check`.
