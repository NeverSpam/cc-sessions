### Step 3: Commit and Merge (Multi-Repo Services Structure)

**PROCESS**: Commit changes in each affected service repo, then optionally create PRs

This workspace uses independent sibling repositories for each service. Unlike submodules, these are fully independent git repos that happen to be related by the task.

#### For Each Service Repo in the Task's `repos` List:

1. Navigate to the service repo: `cd {services_root}/<repo-name>`

2. Check if there are changes to commit:
   ```bash
   git status
   ```
   If no changes, skip to next repo.

3. Stage changes:
   {staging_instructions}

4. Commit with descriptive message:

   {commit_style_guidance}

5. Ask about pushing and PR:
   ```markdown
   [DECISION: Push {repo-name} to Remote]
   Would you like to push the changes and create a PR?
   - PUSH: Push to origin (can create PR later)
   - PR: Push and create PR now
   - NO: Keep changes local only

   Your choice:
   ```

6. If PR selected, create PR with:
   - Title referencing the Linear issue
   - Description summarizing changes in this specific repo
   - Link to related PRs in other repos if applicable

#### After All Service Repos Are Processed:

Return to the workspace directory and update the task file with links to any PRs created.

**Important Notes:**
- Each service repo gets its own commit and potentially its own PR
- PRs can be linked together via description references
- Infrastructure repos should typically be merged before backend repos
- Consider dependency order when merging (infrastructure → backend → frontend)
