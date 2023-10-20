# GIT

## Branch naming

Create branches with a prefix to categorize your branch.

- Task => `feature/`
- Bug => `bugfix/`

Then you should include the ticket number followed by a text describing the change.

e.g.: for ticket 4504 of the type Task with the name "**More detailed logging**" this would look like this: 
`feature/4504-more-detailed-logging`

## Commits

Commits should be kept small and not contain too many different changes.

### Commit subject
- Should always describe briefly and clearly what has been changed. 
- maximum 50 characters.
- Another developer should understand what was done at first glance.

### Commit description

    #Ticket-number Long-description-text

The ticket number must start with a `#` and be followed by a space, then the commit will be linked to the ticket in Azure DevOps.

## Commit Best Practices

https://gist.github.com/luismts/495d982e8c5b1a0ced4a57cf3d93cf60#file-gitcommitbestpractices-md

## Pull Requests

### Before creating a PR

The task should be tested in detail by the developer.

### Creating a PR

- A PR should always have a reviewer 
- A ticket must always be linked
- It is important to follow the PR checklist
- A description of the test cases must always be attached. This can be documented using a description, screenshots and example URLs.
