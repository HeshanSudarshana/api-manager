# Add Issues to Project Workflow

This workflow (`add-issues-to-project.yml`) is designed to automatically find all issues labeled with "4.6.0-BugFixingEffort" and add them to the specified GitHub Project if they aren't already included.

## How to Use

1. **Manual Trigger**: This workflow uses `workflow_dispatch`, meaning it must be triggered manually from the GitHub Actions tab in your repository.

2. **Navigation**: Go to your repository → Actions tab → "Add Bug Fixing Issues to Project" workflow → "Run workflow" button.

## What It Does

1. **Finds Issues**: Searches for all issues (open and closed) with the label "4.6.0-BugFixingEffort"
2. **Checks Project**: For each issue, checks if it's already in the specified GitHub Project
3. **Adds Missing Issues**: Adds any issues that aren't already in the project
4. **Provides Feedback**: Shows which issues were already in the project and which were newly added

## Requirements

### Permissions
The workflow requires the following permissions which are automatically granted:
- `issues: read` - to fetch issues with the specific label
- `contents: read` - to checkout the repository
- `repository-projects: write` - to add items to GitHub Projects

### Project Setup
- The project URL is currently set to: `https://github.com/users/HeshanSudarshana/projects/1`
- This should be a GitHub Projects V2 project (the new project experience)
- The project should be accessible by the repository's workflows

## Customization

To modify this workflow for different labels or projects:

1. **Change the Label**: Update the label name in the API call:
   ```bash
   --field labels="YOUR-LABEL-HERE"
   ```

2. **Change the Project**: Update the project number in the GraphQL query:
   ```graphql
   select(.number == YOUR-PROJECT-NUMBER)
   ```

3. **Change the Owner**: Update the owner name in the query:
   ```bash
   -f owner="YOUR-USERNAME-HERE"
   ```

## Troubleshooting

- **Permission Errors**: Ensure the repository has access to the specified project
- **Project Not Found**: Verify the project number and owner name are correct
- **GraphQL Errors**: Check that you're using GitHub Projects V2 (not the legacy projects)

## Output

The workflow will output:
- Total number of issues found with the label
- Which issues were already in the project
- Which issues were newly added
- Any errors encountered during the process