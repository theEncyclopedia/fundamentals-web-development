# Git guide

Git is the most commonly used version control system in 2000s to 2020s.

## Using a git professionally.

This section is about "How we should use git effective/conventionally".

### What is a perfect Commit ?

A Perfect commit is a well-messaged commit that contains the right changes.

- Seperate your commits into correct packets
  - In 1 issue there might be many changes. After issue is solved reviewing a big PR is a difficult and requires a lot of time. So dividing each changes into seperated commits will help reviewers to review your PR fast and efficient.
- Comment your commit perfectly.
  - The conventions of commenting a commit has a 2 parts. SUBJECT and BODY - Subject must contain concise summary of what happend - Body must contain more detailed explanation - What is now diffrent than before ? - Why ? - Is there anything to watch out for/ anything particularly remarkable ?

### Creating commit

1.First up see what files have changed.

```
// Shows what branch is being used and lists of changes.
git status

// Shows exactly what is changed on that file.
git diff [file_name]
```

2. Select your changes into staged change.

```
// Adding a certain files.
git add [file_name]

// Adding all changes to staged changes.
git add .

// Partially selecting changes into staged change.
// P flag brings us down to the patch level.
// By using this command each changes will be asked to added into staged changes or not.
git add -p [file_name]
```

3. Commenting commit

```
git commit -m ""

git commit -am ""
```

### Branching strategies

### Pull requests

### Merge conflicts

### Merge vs Rebase
