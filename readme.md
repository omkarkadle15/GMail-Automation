# Gmail API Python Script with Optional Attachments

This project demonstrates how to use the Gmail API to send emails, with or without attachments, using Python. Follow these steps to set up and run the script.

## Prerequisites

- Python 3.6 or higher
- pip (Python package installer)
- A Google Cloud account

## Setup

1. Create a Google Cloud Account
   - Go to [Google Cloud Console](https://console.cloud.google.com/)
   - Click on "Create account" or "Sign up" and follow the prompts

2. Create a New Project
   - In the Google Cloud Console, click on the project drop-down and select "New Project"
   - Give your project a name and click "Create"

3. Enable the Gmail API
   - In your project, go to the Navigation menu and select "APIs & Services" > "Library"
   - Search for "Gmail API" and click on it
   - Click "Enable"

4. Create Credentials
   - Go to "APIs & Services" > "Credentials"
   - Click "Create Credentials" and select "OAuth client ID"
   - Choose "Desktop app" as the application type
   - Download the client configuration file and rename it to `credentials.json`

5. Configure OAuth Consent Screen
   - Go to "APIs & Services" > "OAuth consent screen"
   - Choose "External" user type (unless you're using Google Workspace)
   - Fill in the required information (App name, User support email, Developer contact information)
   - Add the necessary scopes (see the "Scopes" section below)
   - Add test users (see the "Adding Test Users" section below)

6. Set Up the Project
   - Clone this repository or create a new directory for your project
   - Place the `credentials.json` file in the same directory as the script

7. Install Required Libraries
   - Ensure you have the `requirements.txt` file in your project directory
   - Run the following command to install the required packages:
     ```
     pip install -r requirements.txt
     ```

## Scopes

This script uses the following Gmail API scope:

```python
SCOPES = ['https://www.googleapis.com/auth/gmail.send']
```

This scope allows the application to send emails on behalf of the authenticated user. If you need to modify the scope:

1. Update the `SCOPES` variable in the script
2. Delete the `token.json` file (if it exists)
3. Update the scopes in the Google Cloud Console under "APIs & Services" > "OAuth consent screen"

## Adding Test Users

While your application is in testing, you need to add test users who can authenticate and use your app:

1. Go to the Google Cloud Console
2. Navigate to "APIs & Services" > "OAuth consent screen"
3. Scroll down to the "Test users" section
4. Click "Add users"
5. Enter the email addresses of your test users (including your own)
6. Click "Save"

Note: Test users must have a Google account. If your application is in testing mode, only these added test users will be able to authenticate and use your application.

## Usage

1. Update the `main()` function in `gmail.py` with your desired sender, recipient, subject, and message body.

2. To send an email without attachments:
   ```python
   message = create_message(sender, to, subject, message_text)
   send_message(service, "me", message)
   ```

3. To send an email with attachments:
   ```python
   file_paths = ["/path/to/attachment1.pdf", "/path/to/attachment2.jpg"]
   message = create_message(sender, to, subject, message_text, file_paths)
   send_message(service, "me", message)
   ```

4. Run the script:
   ```
   python gmail.py
   ```

5. On first run, the script will open a new browser window asking you to authorize the application. Log in with your Google account (must be a test user) and grant the requested permissions.

6. The script will create a `token.json` file to store your access token for future runs.

7. Check the console output for the sent message ID or any error messages.

## File Description

- `gmail.py`: The main Python script that interacts with the Gmail API to send emails with or without attachments.
- `requirements.txt`: Lists all the Python packages required to run the script.

## Functions

- `get_gmail_service()`: Handles authentication and creates the Gmail API service object.
- `create_message(sender, to, subject, message_text, file_paths=None)`: Creates an email message, optionally with attachments.
- `send_message(service, user_id, message)`: Sends the email message.
- `main()`: The main function that demonstrates how to use the script.

## Note

- Keep your `credentials.json` and `token.json` files secure and do not share them publicly.
- If you modify the SCOPES, delete the `token.json` file and re-authenticate.
- Ensure all users of your application (including yourself) are added as test users while the app is in testing mode.
- When adding attachments, make sure to provide the full file path and that the files exist at the specified locations.

## Troubleshooting

If you encounter any issues:
- Ensure you've enabled the Gmail API for your project
- Check that your `credentials.json` file is in the correct location
- Verify that you've granted the necessary permissions during the OAuth flow
- Confirm that you're using a Google account that's been added as a test user
- If you get a "400 Bad Request" error, ensure your OAuth consent screen is properly configured
- For attachment issues, double-check the file paths and ensure the files exist and are accessible
- If you get import errors, make sure you've installed all required packages using `pip install -r requirements.txt`

For more information, refer to the [Gmail API Python Quickstart](https://developers.google.com/gmail/api/quickstart/python) guide.