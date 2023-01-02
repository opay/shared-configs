<a href="https://www.opay.eu" target="_blank"><img src="https://avatars.githubusercontent.com/u/24718711?s=128" width="100" alt="OPAY"></a>

OPAY shared configurations
============

- This repository is used to store shared configuration used in development process.
- Any of this configuration might be used by:
  - Internal (private) projects and repositories;
  - External or public projects and repositories;
  - Our customers and users;
  - Anyone who will find it on Git network and find it useful.
- All the code, history, pull requests, etc. are public and visible for anyone.
- __Any confidential information including paths of private projects and other insides CAN NOT be stored in this repository or pushed as PR.__

## Structure
- `workflows` - shared GitHub workflows used in our public and private projects.
- `bash_scripts` - any king of useful bash scripts used in development process.
- `examples` - any kind of code or configuration examples.

## Bash scripts
- Any internal information including paths inside private projects can't be exposed. Use variables to set private data after downloading script.
- Every script must have short description in comments form in the top of script.

## Workflows
- Paths inside of projects that use shared workflows must be set using `inputs` configuration and hold `_path` suffix. No paths can be set directly in workflows unless default values are used.
- Secrets (credentials, tokens, passwords, etc.) mus be set using `secrets` configuration and can't be exposed even if default values are used.
- Any other internal data must be set using `inputs` or `secrets` configuration.
- Example of usage shared workflow in other projects can be found in [examples/pull_request_workflow.yml](examples/pull_request_workflow.yml)

### Testing workflows
1. Push workflow branch to GitHub
2. Edit other project workflow to use shared workflow from new branch instead of `main`
   - I.e. in [examples/pull_request_workflow.yml](examples/pull_request_workflow.yml) replace `uses: opay/shared-configs/.github/workflows/app_testing.yml@main` to `uses: opay/shared-configs/.github/workflows/app_testing.yml@NEW_BRANCH_NAME`
3. Create pull request with only required workflow update. Actions using shared workflow from development branch will be launched.
4. If test fails, shared workflow can be updated, pushed to GH and test workflow re-run.
5. When testing is finished, Pull Request created for workflow testing should be closed.
