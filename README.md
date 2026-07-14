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

Every frame of the film lives in this repo as a flat, shapeless project:
`frames/frame-0001.csproj` … `frames/frame-6562.csproj`, each pinning the 64
packages exactly one frame behind. Nothing in those files contains a picture.
When Dependabot updates one to the latest versions, **the bot writes the
image**: the red side of its diff is the previous frame, the green side is the
new one.

## The gallery

GitHub's hosted Dependabot watches the `gallery/` folders — frames
**525 · 1444 · 2429 · 3413 · 4398 · 5645** — via `.github/dependabot.yml`.
Each entry carries an `ignore` cap that hides every version beyond its own
frame, so its pull request is never superseded: the PRs stay open forever.
They are never merged. The open PR list *is* the exhibition.

A hosted update run cannot process 6,562 projects, so the full `frames/` reel
is processed by the same engine — [dependabot-cli](https://github.com/dependabot/cli),
one frame at a time — to produce the complete video.

## FAQ

**Is this real?** Yes. The packages are real, the versions are real, and the
gallery PRs are authored by the real `dependabot[bot]` running on GitHub's
infrastructure. Click any open PR and check the Files changed tab.

**Why prerelease tags?** They're the only part of a version string long enough
and free enough to hold 90 pixels. Consecutive dots are invalid SemVer, hence
the `.i` texture for empty space.
