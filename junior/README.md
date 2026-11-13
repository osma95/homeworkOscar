# DevOps Engineer Homework

This starter contains three intentional issues. Allow approximately one hour
to troubleshoot them, verify your changes, and submit your work.

## Requirements

- Bash on Linux, macOS, WSL, or Git Bash on Windows.
- Git and a GitHub account with permission to run GitHub Actions.
- No cloud account, credentials, or additional packages are needed.

Run the commands below from the repository root in Bash.

## Task 1: Fix a failing script (15 minutes)

```bash
bash task-1-script/random-data.sh
```

Correct the failure and explain what the script is doing.

## Task 2: Resolve a configuration issue (15 minutes)

```bash
bash task-2-configuration/show-service.sh
```

This script runs from the repository root but fails from another directory.
Make it work regardless of the caller's working directory. Successful runs
must print `Service: sample-worker` and `Environment: test`.

To reproduce the other-directory behavior:

```bash
repo_root="$(pwd)"
(cd .. && bash "$repo_root/task-2-configuration/show-service.sh")
```

Also verify that a missing configuration produces a useful error and a nonzero
exit code. Restore the configuration after testing.

## Task 3: Repair the automated check (20 minutes)

Review `.github/workflows/check-scripts.yml` and the GitHub Actions logs.
Fix the workflow so both corrected scripts run successfully. Keep the push
and pull request triggers, and ensure a script failure fails the workflow.

## Submission (10 minutes)

- Create your own repository from this starter, or fork it if permitted.
- Make your fixes on a branch, commit and push them, and open a pull request
  against your repository's default branch. Leave it open for review.
- Add a short findings section to this README describing each issue, how you
  identified it, your fix, and the commands or checks used to verify it.
- Provide your repository URL, pull request URL, and a successful Actions run
  URL. For private repositories, grant reviewers access.
- Do not include credentials, secrets, or employer information.

Stop after approximately one hour. If anything remains unresolved, submit
your progress, what you tried, and what you would investigate next.

## Findings

Task 1: Fix a failing script

this script had two typos preventing it to run properly:

echo "Bytes base64: $bytes-base64"
ehho "Bytes base64 count: $bytes_base64_count"

using this variable like this bytes-base64 read "$bytes" as the varioable and the rest as text
ehho makes the script not recognize a valid command

functionality: It generates 10 random bytes, base64-encodes them, counts both, and prints the counts, their sum, and the encoded string.


Task 2: Resolve a configuration issue

config_file="service.conf" resolved relative to the caller’s working directory, so the script failed from any other directory. 
fixed it by resolving the path from ${BASH_SOURCE[0]} so it’s anchored to the script’s own directory.
