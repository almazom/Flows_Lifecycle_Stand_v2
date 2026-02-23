# 🛡️ portable_standalone.md

## What

Ensure the stand is portable and self-contained. No references to external filesystem paths or external URLs in flow artifacts.

## Scope

Applies to:
- `swarm_review/pilot_stand/**`
- run artifacts under `swarm_review/pilot_stand/**/runs/**`
- templates and registries used for run replay

## Contract

```yaml
forbidden_reference_classes:
  - unix_absolute_path
  - macos_absolute_path
  - windows_absolute_path
  - external_http_url
  - ssh_remote_reference

allowed_reference_style:
  - repository_relative_paths_only
  - local_placeholder_paths_inside_repo

portable_project_reference:
  required_path: 'pilot_projects/006_epub'
  external_repo_links_allowed: false
```

## Pass

- No external absolute paths in artifacts
- No external URLs in stand artifacts
- Pilot project reference uses internal repo path

## Fail

- Any external filesystem link
- Any external URL used as canonical project pointer
