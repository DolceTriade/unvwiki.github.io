---
title: Continuous integration
permalink: /Continuous_integration/
---

Continuous integration (CI) refers to the automated builds that run each
time someone opens or modifies a pull request against, or modifies the
code of, the Unvanquished and Daemon source code repositories on GitHub.

We use the following CI services:

- Appveyor, for building with MSVC on Windows. Its configuration is
  found in the file in the repository root.
- Azure Pipelines. Its configuration is found in the file in the
  repository root. It handles Mac native builds on [macOS
  11.x](https://github.com/actions/virtual-environments/blob/main/images/macos/macos-11-Readme.md)
  and Linux native and NaCl builds on [Ubuntu
  20.04](https://github.com/actions/runner-images/blob/main/images/ubuntu/Ubuntu2004-Readme.md)
  (Focal).
- GitHub CodeQL. Its configuration is found in the file in the
  repository. Its purpose is to scan the source code for
  vulnerabilities, and for that purpose it starts by building the source
  tree using the latest LTS Ubuntu distribution provided by the platform
  ([Ubuntu
  22.04](https://github.com/actions/runner-images/blob/main/images/ubuntu/Ubuntu2004-Readme.md))
  and the default compiler of this platform.

In some Daemon builds, we run the unit tests. These builds have been
configured to use the Release configuration so that the unit tests are
closer to production builds.

## Build matrix

<table>
<thead>
<tr class="header">
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Service</p></td>
</tr>
<tr class="even">
<td><p>Appveyor</p></td>
</tr>
<tr class="odd">
<td><p>Appveyor</p></td>
</tr>
<tr class="even">
<td><p>Azure Pipelines</p></td>
</tr>
<tr class="odd">
<td><p>Azure Pipelines</p></td>
</tr>
<tr class="even">
<td><p>Azure Pipelines</p></td>
</tr>
<tr class="odd">
<td><p>Azure Pipelines</p></td>
</tr>
<tr class="even">
<td><p>GitHub Actions CodeQL</p></td>
</tr>
</tbody>
</table>


{\| ! colspan="8" \| \|- ! Service ! Host ! Target ! Compiler !
Generator ! Build Type ! WERROR ! PCH \|- \| Appveyor \|\| Windows amd64
\|\| Windows i686 DLL \|\| VS 2019 \|\| Visual Studio \|\| Debug \|\|
Yes \|\| No \|- \| Azure Pipelines \|\| Ubuntu-20.04 amd64 \|\| Linux
amd64 DLL \|\| GCC 8.4 \|\| Ninja \|\| Debug \|\| Yes \|\| No \|- \|
Azure Pipelines \|\| Ubuntu-20.04 amd64 \|\| Linux amd64 DLL \|\| Clang
11.0 \|\| Ninja \|\| Debug \|\| Yes \|\| No \|- \| Azure Pipelines \|\|
Ubuntu-20.04 amd64 \|\| NaCl all NEXE \|\| PNaCl Clang 3.6 \|\| Ninja
\|\| Debug \|\| Yes \|\| No \|- \| Azure Pipelines \|\| macOS-12 amd64
\|\| macOS amd64 DLL \|\| AppleClang 14.0 \|\| Make \|\| Debug \|\| Yes
\|\| No \|- \| GitHub Actions CodeQL \|\| ubuntu-latest \|\| Linux amd64
DLL+EXE \|\| GCC (floating) \|\| Ninja \|\| Release \|\| No \|\| Yes \|}

“WERROR” indicates whether the option is on, which gives a failing
building build status if there are warnings in our code. Note that only
applies to ”our” code in , so you may still see warnings from stuff in .

“PCH” indicates whether the precompiled header is enabled.

[Category:Infrastructure](Category:Infrastructure "wikilink")