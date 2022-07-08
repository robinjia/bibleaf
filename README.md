# Bibleaf
A tool for managing BibTeX bibliographies with Overleaf documents.

## Setup
Setup is as simple as running:

```
./bibleaf setup
```

## Usage 
1. Add an overleaf project:

```
./bibleaf add [project_name] [overleaf_id]
```
The overleaf ID is what comes after `https://www.overleaf.com/project/` in the Overleaf URL.
The name can be anything you want but must be unique across all your projects.

Running this command will pull the contents of this project and store them in `overleaf/[project_name]`

2. Update the project:

```
./bibleaf update [project_name]
```

This command does the following:
- Pull the Overleaf repository.
- Scan the `.tex` files for all citations.
- Attempt to match each citation with a known BibTeX reference from (in order of priority): 
    - Your custom BibTeX file in `custom.bib`
    - The ACL Anthology (A cached copy of the official ACL Anthology BibTeX is stored in `files/`)
- If some references were not found, issue a warning and stop. (Force completion of the command anyways with `-f`).
- Gather the needed BibTeX references into one file called `refs.bib` and push that file to the Overleaf repository.

## Other utilities

Update the cached ACL anthology BibTeX:

```
./bibleaf pull-acl
```

List all projects:
```
./bibleaf list
```

## Saving your Overleaf account information
To avoid having to type your Overleaf username and password every time you pull/push, you can save them in your `~/.gitconfig` with the following:

```
git config --global credential.https://git.overleaf.com.username [your email address]
git config --global credential.https://git.overleaf.com.helper store
```

Note that you can only run the first command to store your email address but prompt for a password every time.
