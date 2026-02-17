# gh-gl-mirror-action

Reusable GitHub Action that mirrors your GitHub repositories to GitLab: lists repos, creates GitLab projects if needed, and pushes a full mirror of each.

## Usage

In a workflow:

```yaml
- uses: wozniakpl/gh-gl-mirror-action@main
  with:
    gh_pat: ${{ secrets.GH_PAT }}
    gl_pat: ${{ secrets.GL_PAT }}
    gitlab_user: 'your-gitlab-username'
    visibility: 'private'          # public | private | internal
    repository_owner: ${{ github.repository_owner }}
    skip_repos: 'repo-a,repo-b'   # optional, comma-separated repos to exclude
```

## Inputs

| Input | Required | Description |
|-------|----------|-------------|
| `gh_pat` | Yes | GitHub PAT (repo scope or fine-grained read) |
| `gl_pat` | Yes | GitLab PAT (api or read_repository + write_repository) |
| `gitlab_user` | Yes | GitLab username |
| `visibility` | Yes | New GitLab project visibility: `public`, `private`, `internal` |
| `repository_owner` | Yes | GitHub user/org whose repos to mirror |
| `skip_repos` | No | Comma-separated repo names to exclude (e.g. the repo that runs this workflow) |
| `skip_failed_repos` | No | If `true`, continue with the next repo when one fails instead of failing the job (default `false`) |

## Token permissions

- **GitHub PAT:** Classic scope `repo`, or fine-grained: Contents (Read), Metadata (Read).
- **GitLab PAT:** Scopes `api`, or `read_repository` + `write_repository`.

This action does not need to be used from the same account that owns the mirrored repos; pass the owner via `repository_owner` and a PAT that can list and clone those repos.
