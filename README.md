# git-hooks

## Step 1

Make a repository on github!

## Step 2 

Clone the repo to your pc!


## Step 3

Navigate to your local Git repository's .git/hooks directory:

```
cd <your_repository_directory>/.git/hooks
```

## Step 4

Create the commit-msg file (without an extension) if it doesn't already exist:

```
touch commit-msg
```

## Step 5

Make the commit-msg file executable:

```
chmod +x commit-msg
```

## Step 6

Open the commit-msg file in a text editor (you can use any text editor you prefer):


```
nano commit-msg
```

## Step 7

Add the following code to the commit-msg file:

```
#!/bin/bash

COMMIT_MSG_FILE=$1
COMMIT_MSG=$(cat $COMMIT_MSG_FILE)

# Define the regex pattern for the commit message format
COMMIT_MSG_PATTERN="^(feature|fix|refactor|wip): .{1,50}$"

# Check if the commit message matches the pattern
if ! [[ $COMMIT_MSG =~ $COMMIT_MSG_PATTERN ]]; then
    echo "Error: Commit message format is invalid. Please use '<type>: <description>' (max 50 characters)."
    exit 1
fi
```

## Step 8

Save the file and exit the text editor.

## Step 9

Test the Hook

Make a new commit with a commit message that violates the format (e.g., too long or incorrect format):

```
git commit -m "Added a new feature that does a lot of things and is too long for the format"
```

The hook should reject the commit and display an error message.

# Step 10

Once you've verified that the hook works as expected, push your local changes to the GitHub repository:

```
git push origin main
```