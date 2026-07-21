# Bad Apple!!, but it's Dependabot

You know Bad Apple!! — the black-and-white silhouette animation that people have
rendered on oscilloscopes, in Minecraft, on pregnancy tests, and inside every
piece of software that has ever had a screen.

This is Bad Apple!! playing inside the **"Files changed" tab of pull requests**,
where every single frame is drawn by `dependabot[bot]`. Not by me. By the bot.
I just gave it no other choice.

![One frame, drawn by Dependabot](preview.png)

Every open PR in this repo is one frame of the video. Open any of them, hit
"Files changed", squint a little, and you're looking at Marisa Kirisame made
out of NuGet package versions.

## How?

I published **419,968 NuGet packages.**

I need you to sit with that number for a second. Four hundred and nineteen
thousand, nine hundred and sixty-eight real, installable, publicly-listed NuGet
packages, each one a valid `netstandard2.0` library that does absolutely
nothing. My GitHub packages page loads like it's trying to summon something.

Here's the actual trick.

The film is 6,562 frames. Each frame is **its own branch** (`frame-0001` …
`frame-6562`), and each branch contains exactly one shapeless project file that
pins 64 tiny packages — one per row of pixels — at a boring clean version:

```xml
<PackageReference Include="BAF0525L00" Version="1.525.0-0" />
<PackageReference Include="BAF0525L01" Version="1.525.0-0" />
<!-- ...62 more... -->
```

**No file in this repo contains any image data.** The branches are blank
canvases. The picture lives entirely in a *newer version* of each package that
I also published — one whose prerelease tag is a row of pixels:

```
1.525.0-0                                          ← the pin (a blank row)
1.525.0-i.i.i.i.iMMMMMMMMMMMMMMMM.i.i.i.i.i.i.i.ii ← the drawing (M = ink)
```

Both are perfectly valid SemVer2. And here's the part that makes the bot
complicit: SemVer says a pinned prerelease can **only** be updated to a newer
prerelease of the same release. So the one and only move Dependabot is allowed
to make is `-0` → `-that horrible pixel string`. It doesn't know it's painting.
It thinks it's doing security hygiene. Every drop of ink in every diff was typed
by the bot, believing it was helping.

I register all 6,562 branches with Dependabot, it opens a pull request for each,
and the open-PR list becomes a flip-book. The PRs are **never merged** — merging
would end the exhibit. The gallery *is* the backlog.

## Why 419,968 packages though. Genuinely why.

Because I tried it the sane way first, and Dependabot fell over.

Version one used just 64 shared packages for the whole film. Problem: every
frame adds two versions to each package, so halfway through, each package had
~11,000 versions. To pick an update, a NuGet client downloads the *entire
version list* — a 450 KB wall of text — and Dependabot's jobs started timing out
and dying before they could draw anything.

The fix: give every frame its own 64 packages (`BAF<frame>L<row>`). Now each
package has exactly two versions, forever, and Dependabot resolves each one
instantly. The cost of "instantly" is 6,562 × 64 = **419,968 packages.** Worth
it. Would do it again. Have not slept.

## FAQ

**Is this real or did you Photoshop the PRs?** Real. The packages are real, the
versions are real, and the pull requests were authored by the actual
`dependabot[bot]` running on GitHub's own servers. Click any PR → Files changed.
Check the author. It's the bot. It has no idea.

**Why the `.i.i.i` gunk in the empty parts?** Because two dots in a row (`..`)
is invalid SemVer, and a hyphen renders as a solid line. `.i` is the least-ugly
legal way to say "background" — a faint dotted texture that runs the full width
of every row.

**How long until all 6,562 are up?** Roughly a week of Dependabot grinding away.
GitHub only runs so many update jobs at once, so the reel fills in at its own
patient pace. The open-PR count is the progress bar.

**Did NuGet ban you?** These are on **GitHub Packages**, not nuget.org. I'm not
*that* reckless. (Please don't tell them.)

**Why?** Wrong question.
