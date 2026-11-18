# Coordinating public releases

SugarCasino maintains three public repositories:

- [ts-sdks](https://github.com/SugarCasino/ts-sdks) contains the public npm packages `@sugar/sdk`, `@sugar/mcp`, and `@sugar/suifrens-display-system`.
- [agent-skills](https://github.com/SugarCasino/agent-skills) contains the full skills and their references. It is installed through the skills CLI, not published as an npm package.
- [.github](https://github.com/SugarCasino/.github) contains organization community files and the public profile. It has no npm release.

## Before publishing npm packages

1. Merge the matching skills into `agent-skills/main`. Each SDK package includes a small skill entry that fetches instructions and references from that branch, independently of its npm version. Check that all linked skills and references are available there and that the instructions match the package being released.
2. Merge the matching community/profile updates into `.github/main`. Public links use the default `main` branch, not a temporary PR branch. Package documentation links become available when the SDK workspace lands on `ts-sdks/main`.
3. In `ts-sdks`, include changesets for all changed public packages and pass the package checks and publication identity check before merging. The Changesets workflow creates a version PR or publishes from main. Check the active prerelease mode and npm dist-tag: a beta release must be installed using its beta tag or exact version until a stable latest release exists.
4. Configure npm publishing authorization for the repository and verify ownership of the package scope before the first release. Source names and `publishConfig.access: public` alone do not prove that registry authorization is ready.
5. After npm publication, verify package availability and the skill URLs. The MCP Registry workflow runs only when Changesets reports a published `@sugar/mcp`, and waits for that version on npm.

Skill metadata versions are separate from package versions. Do not advertise unimplemented exports or infer that an npm release exists from a public GitHub repository. Keep existing application version pins unless an upgrade is requested.

## Public contributions

All three repositories allow external contributions. Recognized SugarCasino members must use GitHub noreply addresses; external contributors may retain their own names and emails. The publication check uses read-only repository access and does not grant merge approval, write access, or publishing rights. See [the identity policy](git-publication-privacy.md).
