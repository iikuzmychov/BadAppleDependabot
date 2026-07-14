# Bad Apple!!, but it's Dependabot

Every open pull request in this repo is one frame of Bad Apple!!, drawn by
`dependabot[bot]` itself.

![Frame 525, drawn by Dependabot](preview.png)

## How it works

The animation is encoded in NuGet package versions. There are 64 packages,
[`BadApple.R00`…`R63`](https://github.com/iikuzmychov?tab=packages), one per
pixel row, and each published version looks like:

```
1.525.0-i.i.i.i.i.i.iMMMMMMMMMMMMMMMM.i.i.iMMMMMMM
```

The prerelease tag encodes the pixels of that row — `M` is ink, `.i` is
background, the string ends at the row's last bright pixel, and the minor
version is the frame number. All of it is valid SemVer2.

Every frame of the film lives in this repo: `frames/frame-0001/` …
`frames/frame-6562/`, each a single shapeless project pinning the 64 packages
at the clean `1.<frame>.0-0` — **no file in this repo contains any image
data**. When Dependabot updates a frame to `1.<frame>.0-<strip>`, every drop
of ink in the diff was written by the bot.

All 6,562 frames are registered with Dependabot (`.github/dependabot.yml`).
Since a pinned prerelease can only move to a newer prerelease of the same
release, each folder's PR draws exactly its own frame and is never superseded.
The PRs are never merged — the open PR list *is* the exhibition, and it grows
as Dependabot works through the reel.

## FAQ

**Is this real?** Yes. The packages are real, the versions are real, and the
PRs are authored by the real `dependabot[bot]` running on GitHub's
infrastructure. Click any open PR and check the Files changed tab.

**Why prerelease tags?** They're the only part of a version string long enough
and free enough to hold 90 pixels. Consecutive dots are invalid SemVer, hence
the `.i` texture for empty space.
