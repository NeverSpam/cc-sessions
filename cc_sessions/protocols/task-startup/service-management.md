### Multi-Repo Service Management

**CRITICAL: Create matching branches in ALL affected service repos**

This workspace manages multiple independent git repositories as sibling directories. Each service repo (backend, infrastructure, etc.) is a separate git repository.

- Check the task frontmatter for the `repos` list
- For each repo listed in `repos`:
  1. Navigate to the service repo directory: `cd {services_root}/<repo-name>`
  2. Verify it's a git repository (`.git` directory exists)
  3. Check for uncommitted changes first and, if any, ask user how to handle them
  4. If not on {default_branch}, checkout {default_branch} and pull latest (do not destroy uncommitted changes)
  5. Create a branch with the same name as the task branch (from frontmatter)
  6. Return to the workspace directory

**Example**: If working on task with `branch: feature/al-123-mailbox-sync` and `repos: [mailboxes-backend, mailboxes-infrastructure]`:
1. `cd {services_root}/mailboxes-backend && git checkout {default_branch} && git pull && git checkout -b feature/al-123-mailbox-sync`
2. `cd {services_root}/mailboxes-infrastructure && git checkout {default_branch} && git pull && git checkout -b feature/al-123-mailbox-sync`

**Branch Discipline Rules:**
- Task frontmatter must list ALL repos that might be edited during this task
- All listed repos MUST have matching task branches before any edits
- Before editing any file, verify the containing repo is on the correct branch
- If a repo needs to be added mid-task, create its branch immediately and update the task frontmatter

**Linear Integration:**
- Branch names should match the Linear issue branch (e.g., `feature/al-123-description`)
- This ensures PRs are automatically linked to Linear issues
- LaunchDarkly feature flags can reference the branch/issue name
