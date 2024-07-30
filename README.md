# Code of Conduct Analyzer GitHub Action

This GitHub Action checks for the presence of `CODE_OF_CONDUCT.md` in a repository, processes its content, and takes appropriate actions based on the analysis.

## Features

- Checks for the existence of `CODE_OF_CONDUCT.md` in the repository.
- Sends the content of `CODE_OF_CONDUCT.md` to an external server for analysis.
- Takes actions based on the analysis results, such as creating issues or sending notifications.
- Delegates further processing to other actions.

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
2. **Check for `CODE_OF_CONDUCT.md`**: Verifies if the file exists in the repository.
3. **Analyze the Code of Conduct**: Sends the content of the `CODE_OF_CONDUCT.md` file to an external server for analysis.
4. **Handle Analysis Results**: Based on the analysis results, takes appropriate actions such as creating issues or sending notifications.
5. **Send to Comment Analyzer**: Forwards the analysis results and the comment details to the Comment Analyzer action for further processing.

## Example Scenario
- **Code of Conduct Present and Valid**: The action proceeds with further analysis and sends the results for additional processing.
- **Code of Conduct Missing or Invalid**: The action creates an issue or takes other appropriate actions based on the analysis results.

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

## Author
Created by CobosDS. For any issues or contributions, please open an issue or submit a pull request on the [GitHub repository](https://github.com/SOM-Research/code-of-conduct-analyzer).
