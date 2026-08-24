# BelongOS releases

Signed, notarized release artifacts for the **BelongOS Mac app**, plus the
[Sparkle](https://sparkle-project.org) appcast the shipped app reads to update
itself.

This repository holds **no source code**. It is public for one reason: the
BelongOS monorepo is private, so its release assets sit behind an auth wall
that Sparkle cannot pass. The feed and the disk images have to be reachable by
an unauthenticated `GET` from a user's Mac, and this is the smallest thing that
makes that true.

## The feed

    https://github.com/computamusic/belongos-releases/releases/latest/download/appcast.xml

`releases/latest/download/<asset>` always resolves to the newest release, so the
URL compiled into the app never changes.

Every disk image is:

- signed with `Developer ID Application: Robert Baker (Q737CGNE6Z)`,
- notarized by Apple and stapled, and
- signed again with the EdDSA key whose public half is compiled into the app
  (`SUPublicEDKey`). Sparkle verifies that signature before it unpacks
  anything, so an artifact swapped out here still cannot install.

## Downloads

The newest disk image is always on the
[releases page](https://github.com/computamusic/belongos-releases/releases/latest).

Builds before 1.0.2 do not contain Sparkle and cannot update themselves —
download 1.0.2 or later once, and updates are automatic from there.

## Publishing

Releases are cut from the monorepo, never by hand:

    scripts/release/mac-release.sh <version>
