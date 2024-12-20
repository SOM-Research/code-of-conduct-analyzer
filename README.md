# Code of Conduct Analyzer GitHub Action

This GitHub Action checks for the presence of `CODE_OF_CONDUCT.md` in a repository, processes its content, and takes appropriate actions based on the analysis.

## Features

- Checks for the existence of `CODE_OF_CONDUCT.md` in the repository.
- Sends the content of `CODE_OF_CONDUCT.md` to an external server for analysis.
- Delegates further actions based on the analysis results to other actions.
- Integrates with other GitHub Actions to handle specific scenarios:
  - `code-of-conduct-initializer` for adding or updating the Code of Conduct.
  - `issue-manager` for creating issues if the Code of Conduct is incomplete or missing guidelines.
  - `comment-analyzer` for analyzing and handling comments based on the analysis.

## Inputs

- `GITHUB_TOKEN` **(required)**: GitHub token for authentication.
- `SERVER` **(required)**: Server URL to send the code of conduct for analysis.
- `bot_user` **(required)**: GitHub bot user for performing automated actions.
- `sendinblue_api_key` **(required)**: Sendinblue API key for sending email notifications.
- `email_from` **(required)**: Sender email address for notifications.
- `email_to` **(required)**: Recipient email address for notifications.
- `bot_token` **(required)**: GitHub token of the bot for performing actions.

### How It Works
1. **Checkout Repository**: The action checks out the repository to get the latest code and context.
2. **Check for Bot User**: Determines if the actor is the bot user to prevent self-triggering.
3. **Save Comment Details**: The action saves the details of the comment to a JSON file.
4. **Check for `CODE_OF_CONDUCT.md`**: Verifies if the file exists in the repository.
   - If missing, triggers `code-of-conduct-initializer` to add the Code of Conduct and stops further actions.
5. **Analyze the Code of Conduct**: Sends the content of the `CODE_OF_CONDUCT.md` file to an external server for analysis.
6. **Handle Analysis Results**: Based on the analysis results, takes appropriate actions such as creating issues or sending notifications.
   - If the Code of Conduct has fewer than 5 lines, triggers `issue-manager` to create an issue for incomplete Code of Conduct and stops further actions.
7. **Forward Analysis Results**: Sends the comment details and analysis flags to the `comment-analyzer` action for further processing.
8. **Calculate Missing Flags**: Determines which guidelines are missing from the Code of Conduct.
   - If any guidelines are missing, triggers `issue-manager` to create an issue for the missing guidelines.
9. **Check Contributor Covenant Version**: Determines if the Code of Conduct is based on an outdated version of the Contributor Covenant.
   - If outdated, triggers `code-of-conduct-initializer` to update the Code of Conduct.

## Example Scenario
- **Missing Code of Conduct**: The action will add a `CODE_OF_CONDUCT.md` file and create a pull request.
- **Incomplete Code of Conduct**: The action will create an issue indicating that the Code of Conduct is incomplete and requires more details.
- **Outdated Code of Conduct**: The action will update the `CODE_OF_CONDUCT.md` to the latest version and create a pull request.

## Permissions
This action requires the following permissions:

- `contents: write`
- `issues: write`
- `pull-requests: write`
- `discussions: write`
- `actions: read`

Ensure these permissions are set in your workflow.

## License
This work is licensed under a Creative Commons Attribution-ShareAlike 4.0 International License.

The CC BY-SA license allows users to distribute, remix, adapt, and build upon the material in any medium or format, so long as attribution is given to the creator. The license allows for commercial use. If you remix, adapt, or build upon the material, you must license the modified material under identical terms.

[Creative Commons License](https://creativecommons.org/licenses/by-sa/4.0/)

