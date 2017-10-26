# Task tracking and notes taking in git

This is a template for my simple task logging system.

I decide to describe and share tools and methods that I use for planning and logging completed tasks.

## Tools

1. [Todoist](https://todoist.com/)
1. Logger of completed tasks: [todoist-gist-sync](https://github.com/vikmind/todoist-gist-sync)
1. Couple of shell scripts: [notes-scripts](https://github.com/vikmind/notes-automation)
1. [Clone](https://help.github.com/articles/duplicating-a-repository/) of this repository

## Preparation

All steps should be run inside of this repository's clone.

1. Setup [logger](https://github.com/vikmind/todoist-gist-sync)
1. ``git clone <your-gist-url> tasks``
1. ``git clone git@github.com:vikmind/notes-automation.git scripts``

## How it works

Every sunday I make review of the past week and plan for the next one.
Then during the week I score my progress on goals every evening.

### 1. Creating week

Plans for the week are going to the file ``focus.txt`` in this format:

```txt
Project 1
Goal

Project 2
Goal
```

Then command ``sh ./scripts/create_week.sh`` creates markdown file
for the new week named like ``_Done_2017-10-23_W43.md`` with this content:

```markdown
### 2017 week 43
#### 23.10 - 30.10
* * *
Project|Goal|Mon|Tue|Wed|Thu|Fri|Sat|Sun|All|Complete?
---|---|---|---|---|---|---|---|---|---|---
Project 1   | Goal for project 1 |-|-|-|-|-|-|-|**0.0**|**N**
Project 2   | Goal for project 2 |-|-|-|-|-|-|-|**0.0**|**N**

#### Monday, October 23
```

### 2. Everyday review

Review starts with command ``sh ./scripts/fill_tasks.sh``. Then I check tasks
and score goals progress in current week file's header and save (commit and push) it with
``sh ./scripts/save.sh``

### 3. Weeks review

In the week's end I calculate total score and mark goal as completed or not.
Then command ``sh ./scripts/end_week.sh`` move current week file into ``<YEAR>``
folder and append its header to file ``<YEAR>/Done_<YEAR>.md``

## Couple helpers

### Remind about weekly focus

With command ``sh ./scripts/show_focus.sh`` contents of file ``focus.txt``
will be shown on every new terminal session.

### Log and show YTB status

At my work, we exchange our current statuses in YTB(yesterday, today, block) format.
I usually write them in evening, so I can copy-paste it when I open only one eye ;).
For this purpose you can create reverse-log file named ``_<PROJECT_NAME>_YTB_<YEAR>.txt``
and keep records manually in this format:

```txt
**25.10.2017**
y: some task
another task
t: new task
another new task
b: none

**24.10.2017**
...
```

and show only top-most record with command ``sh ./scripts/cat_ytb.sh <PROJECT_NAME>``
