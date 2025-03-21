**PLACEHOLDER REPO UNTIL I ACTUALLY BUILD IT**

# rubocop-todo-to-done
CLI to autocorrect entries from a `.rubocop_todo.yml` one at a time

## What is this for?

Mass running Rubocop autocorrections on a legacy codebase in a way that makes it
much easier to debug using `git bisect` or `git revert` if something either goes wrong
or goes against the tastes of the existing team.

## Concept

1. `$ rubocop_to_done [--safe/--unsafe] [--only {pattern}]`
2. Asserts there's a `.rubocop_todo.yml` file
3. Asks for branch name (current branch if none)
5. Scans through the todo file for autocorrectable rules matching `{pattern}`
6. For each autocorrectable rule do |rule|
    1. Remove it from the todo file
    2. Safe the ToDo file
    3. `$ rubocop [-a/-A] --only [rule]`
    4. `$ git commit -am 'autocorrect [rule]'`
7. `$ rubocop [-a/-A]`
8. `$ git commit -am 'autocorrect remaining offenses'`
