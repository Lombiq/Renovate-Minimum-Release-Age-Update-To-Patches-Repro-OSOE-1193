# 39472

Minimal repro for https://github.com/renovatebot/renovate/discussions/39472.

Note that the repro uses the `AuralizeBlazor` package as a real-life example since it recently had a similar pair of releases (v3.0.0 and then v3.0.3). But otherwise, this issue is not specific to the package.

## Current behavior

1. My project uses `Dependency` v1.0.0 and has `minimumReleaseAge: '3 days'` configured for major and minor releases, and `0 days` for patch ones.
2. `Dependency` gets a new v2.0.0 released. Renovate does nothing since 3 days haven't yet passed.
3. 2 days pass. `Dependency` gets v2.0.1 released. Renovate does nothing since 3 days haven't yet passed.
4. 1 additional day passes. Renovate opens a PR for v2.0.0 and not v2.0.1.

## Expected behavior

I'd like to achieve a kind of "wait 3 days after a major/minor release, and if there's a patch release since then, update to that when the 3 days pass" behavior. Here's an example of what I'd like to achieve:

1. My project uses `Dependency` v1.0.0 and has `minimumReleaseAge: '3 days'` configured.
2. `Dependency` gets a new v2.0.0 released. Renovate does nothing since 3 days haven't yet passed.
3. 2 days pass. `Dependency` gets v2.0.1 released. Renovate does nothing since 3 days haven't yet passed.
4. 1 additional day passes. Renovate opens a PR for v2.0.1.

And similarly if `Dependency` gets v1.1.0 and then v1.1.1 released.

## Link to the Renovate issue or Discussion

https://github.com/renovatebot/renovate/discussions/39472
