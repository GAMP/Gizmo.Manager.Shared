# Gizmo.Manager.Shared

> **Draft — not ready for restore, build, pack, or publication.**
>
> This repository is a configuration draft for [GHI-1](https://github.com/GAMP/Gizmo.Manager.Shared/issues/1) under the
> canonical [Gizmo.Infra #20](https://github.com/GAMP/Gizmo.Infra/issues/20) NuGet rollout contract. It activates no
> publication and is not ready to be consumed, packed, or released.

## Current state

- **No source files.** The tracked content is `Gizmo.Manager.Shared/Gizmo.Manager.Shared.csproj`, the solution
  `Gizmo.Manager.Shared.sln`, `LICENSE`, `README.md`, `.gitattributes`, and `.gitignore`. The library has no API
  surface, so packaging it today would publish an empty assembly.
- **No known consumers.** GHI-1 discovery found no public or local consumer of `Gizmo.Manager.Shared`; GitHub code
  search and a scan of the local sibling repositories matched only this repository itself. This records the *absence
  of known consumers*, not proof that none exist: private consumers are not observable.
- **Never published.** Discovery observed no `Gizmo.Manager.Shared` package on NuGet.org (flat-container index `404`,
  registry search `0` results) and zero Git tags in this repository. No build, pack, CI run, or publication was
  performed for this draft, so nothing here is packaging evidence.
- **Configuration line only.** `Version` is the canonical line `1.0`, normalized from `1.0.0.0`. It is not a
  published version and asserts no release.

## Known blocker: target-framework conflict (deliberately retained)

- The project targets `netstandard2.0`.
- It keeps an unconditional `ProjectReference` to `..\..\Gizmo.Web.Api.Models\Gizmo.Web.Api.Models.csproj`, a sibling
  checkout outside this repository that targets `net10.0`.
- A `netstandard2.0` project cannot consume a `net10.0` assembly, so restore of this project is expected to fail with a
  NuGet framework-compatibility error (not executed for this draft), and a clean standalone checkout has no sibling
  project to reference at all.
- This conflict is retained on purpose: no target-framework change, no `PackageReference` substitution, no removal of
  the dependency, and no removal of the solution's sibling project entry are included, because that compatibility
  decision remains with the repository owner.

## Deliberately absent from this draft

- **No `.github/workflows/package.yml`.** The canonical caller workflow publishes on `push` to the protected
  `pre-release` and `release` branches, so adding it would activate publication during an owner hold. The migration is
  therefore **staged incompletely**; no disabled, duplicated, or custom publishing workflow is added in its place.
- No `package_icon.png`, although the project declares `<PackageIcon>package_icon.png</PackageIcon>`; `pack` is
  expected to fail (`NU5046`) until the icon is supplied.
- No Trusted Publishing binding, no `NUGET_USER` configuration, no registry reconciliation, and no baseline tag.

## References

- [GHI-1 — Gizmo.Manager.Shared NuGet rollout](https://github.com/GAMP/Gizmo.Manager.Shared/issues/1)
- [Gizmo.Infra #20 — rollout contract](https://github.com/GAMP/Gizmo.Infra/issues/20)
- [Gizmo.Web.Api.Models #10 — upstream dependency (still open)](https://github.com/GAMP/Gizmo.Web.Api.Models/issues/10)
