# Bad Apple!!, but it's Dependabot

Every open pull request in this repo is one frame of Bad Apple!!, drawn by
`dependabot[bot]` itself.

![One frame, drawn by Dependabot](preview.png)

## How it works

Every frame of the film is a branch: `frame-0001` … `frame-6562`, each holding
a single shapeless `frame-<n>.csproj` that pins the frame's 64 row packages,
`BAF<frame>L00` … `BAF<frame>L63`, at the clean `1.<frame>.0-0` — **no file in
this repo contains any image data**.

Each row package has exactly two published versions: the pin, and the row's
pixels.

```
1.525.0-0
1.525.0-i.i.i.i.i.iMMMMMMMMMMMMMMMM.i.i.i.i.i.i.i.i.i.i.i.i.i.i.i.i.i.i.ii
```

In the prerelease tag, `M` is ink and `.i` is background texture, running the
full width of the row — all of it valid SemVer2. A pinned prerelease can only
ever be updated to a newer prerelease of the same release, so the only move
Dependabot can make is `-0` → `-<pixels>`: it has no choice but to paint.

Each branch is registered in `.github/dependabot.yml` as its own update
target, so every frame gets its own pull request into its own branch. The PRs
are never merged — the open PR list *is* the exhibition, and it grows as
Dependabot works through the reel.

## FAQ

**Is this real?** Yes. The packages are real, the versions are real, and the
PRs are authored by the real `dependabot[bot]` running on GitHub's
infrastructure. Open any PR and check the Files changed tab.

**Why prerelease tags?** They're the only part of a version string long and
free enough to hold 90 pixels of a row. Consecutive dots are invalid SemVer,
hence the `.i` background texture.

**Why one package set per frame?** So every package has exactly two versions,
forever — Dependabot resolves each update in seconds no matter how long the
film runs.
