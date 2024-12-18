
# GitHub Repository Access Checker

This project provides a shell script to automate the process of listing users with read access to a specific GitHub repository. The script uses the GitHub API and `jq` for JSON parsing.

## Features

- Fetches and lists all users with read access to a GitHub repository.
- Uses GitHub API authentication via username and personal access token.
- Filters collaborators to display only those with `pull` (read) permissions.

---

## Prerequisites

1. **GitHub Personal Access Token**  
   - Navigate to **GitHub Developer Settings** > **Personal Access Tokens** > **Classic Tokens**.
   - Generate a new token with at least the `repo` permission.
   - Keep the token secure.

2. **Tools and Packages**  
   - Install `curl` and `jq` for HTTP requests and JSON parsing:
     ```bash
     sudo apt install curl jq -y
     ```

3. **Environment Setup**  
   - Export your GitHub username and token as environment variables:
     ```bash
     export username="your_github_username"
     export token="your_personal_access_token"
     ```

---

## Script Overview

### File: `list_users.sh`
This shell script accepts two inputs:
1. **Repository Owner**: The organization or username owning the repository.
2. **Repository Name**: The name of the repository.

### Functions
1. `github_api_get`: Sends a GET request to the GitHub API.
2. `list_users_with_read_access`: Lists collaborators with read access to the specified repository.

### Usage
```bash
./list_users.sh <repository_owner> <repository_name>
```

### Example
```bash
./list_users.sh devops-by-examples python
```

---

## Steps to Deploy

1. **Clone the Repository**
   ```bash
   git clone <repository_link>
   cd <repository_directory>
   ```

2. **Grant Execution Permission**
   ```bash
   chmod +x list_users.sh
   ```

3. **Run the Script**
   ```bash
   ./list_users.sh <repository_owner> <repository_name>
   ```

4. **Output**
   - Displays usernames with read access.
   - If no users are found:
     ```
     No users with read access found for <repository_owner>/<repository_name>.
     ```

---

## Automating for Multiple Repositories

Use a loop to automate the script for multiple repositories:
```bash
for repo in $(cat repo_list.txt); do
    ./list_users.sh <repository_owner> $repo
done
```

---

## Example Cloud Deployment

1. Launch an AWS EC2 Instance.
   - Choose an Ubuntu AMI and connect via SSH.
   - Install required tools:
     ```bash
     sudo apt update && sudo apt install curl jq -y
     ```

2. Clone the repository and execute the script:
   ```bash
   git clone <repository_link>
   cd <repository_directory>
   chmod +x list_users.sh
   ./list_users.sh devops-by-examples python
   ```

3. Output:
   - The script lists all users with read access to the specified repository.

---

## Notes

- Ensure the GitHub personal access token has the necessary permissions for the repositories being queried.
- Use secure methods to store and handle API tokens to avoid exposure.

---

## License

This project is licensed under the MIT License.
