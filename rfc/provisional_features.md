- Abstract

  Currently, the api for all new features in JupyterLab has to be frozen within the span of a single PR. This is due to the fact that we follow semver; breaking changes may only occur on the occasion of a major version bump.

  This is fine for most features. However, this dev process is causing problems when used for complex features. In particular, features that are expected to be adopted community-wide (eg LabIcon, the extension system, anything to do with user settings) have issues:
    - These features (including their API) benefit from wide community feedback, and suffer in the vacumn of 1000+ line single PRs
    - The more complex a feature, the more likely it is for its first draft to have at least some poorly formed or ill-considered API

  To fix this, I propose that we should adopt a formal process for allowing provisional features in the master branch of JuptyerLab core.

- Goals
  - a better experience for core devs, extension devs, and power users around versioning and compatibility
  - easier version migration for core and extensions packages

- Terminology
  - community: JupyterLab core devs, extension devs, and end users
  - API: public interface, including externally visible package structure, function signatures, CLI, and, in the broadest sense, user interface

- Creating a new provisional feature (Python/Typescript sources)
  - Create new feature in PR, as per normal
  - Add a `_PROVISONAL` suffix to all public API
  - Declare the provisional API in the PR issue thread
  - Include an outline of future work, including a rough schedule describing the process by which this feature will graduate by the time of the next major release

- Graduating a feature from provisional to mature
  - A provisional feature may graduate on any minor release
  - A provisional feature must graduate by the next major release (wrt when it was initally pulled into core) or be removed
