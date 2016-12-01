# indesign-upgrade-unbreak
Fix DF015 errors when using RemoteUpdateManager on InDesign &amp; InCopy

This tool fixes missing symlinks left behind by the InDesign and InCopy installers
on macOS. This corrects DF015 errors when installing updates with
RemoteUpdateManager.

## Problem details

Some of the plugins are installed with directories instead of symlinks in their
`Versions` directories and with a directory instead of a symlink at `Resources`.
The `Versions` directory should contain a directory called `A` and a symlink to it
called `Current`, but on broken installations `Current` is a directory.
`Resources` should be a symlink to `Versions/Current/Resources`, but on broken
installations it's also a directory.

Replacing these directories with symlinks makes updates work, but updates
sometimes re-break it, so it's important to run this tool before every
RemoteUpdateManager run.

We opened a case with Adobe after we hit this with CC2014, but as of CC2015 it
has not been fixed. We haven't yet deployed CC2017, so I don't know if it also
suffers from this problem.

## History of this tool

This program was first posted publicly at <https://forums.adobe.com/thread/1942611>

This program originally lived in the private svn repository for our cfengine
deployment. This git repository does not contain version history prior to 0.3,
the first public version (which corresponds to r5410, committed 2015-11-25).
