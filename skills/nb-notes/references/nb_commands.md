# nb Command Reference

## Basic Commands

### Creating Notes

```bash
# Add a markdown note to the claude notebook with tags
nb claude:add --type md --title "Note Title" --tags tag1,tag2,tag3 --content "Note content here"

# Add a note with content from stdin
echo "Note content" | nb claude:add --type md --title "Note Title" --tags tag1,tag2
```

### Creating Todos and Tasks

```bash
# Add a todo item to the claude notebook
nb claude:todo add "Task description" --tags tag1,tag2

# Add a task (nb tasks)
nb claude:tasks add "Task description" --tags tag1,tag2

# List todos
nb claude:todo list

# List tasks
nb claude:tasks list

# Complete a todo
nb claude:todo do <id>

# Complete a task
nb claude:tasks do <id>
```

### Searching Notes

```bash
# Search all notes in claude notebook
nb claude:search "search term"

# Search notes with specific tags
nb claude:search --tags technical-decision

# List all notes in claude notebook
nb claude:list

# List notes with specific tags
nb claude:list --tags session-insight,code-pattern
```

### Editing Notes

```bash
# Edit a note by ID or title
nb claude:edit <id>
nb claude:edit "Note Title"

# Show a specific note
nb claude:show <id>
```

### Viewing Notes

```bash
# Show a note's content
nb claude:show <id>

# Show recent notes
nb claude:list --limit 10
```

## Notebook Structure

All Claude notes go in the `claude` notebook to keep them separate from personal notes.

## Tagging Conventions

Use these standard tags to categorize notes:

- `#technical-decision` - Architectural choices, framework decisions, design rationale
- `#session-insight` - Important learnings or patterns discovered during work
- `#deferred-task` - Issues or improvements to address later (use nb todo/tasks)
- `#code-pattern` - Common patterns, antipatterns, or conventions found in codebases
- `#bug-fix` - Solutions to bugs and their root causes
- `#workflow` - Process improvements or workflow discoveries
- `#preference` - User preferences and working style notes

Multiple tags can be applied to a single note when appropriate.

## Note Title Conventions

- Keep titles concise but descriptive (5-10 words)
- Use present tense verbs for actions ("Use factory pattern for tool creation")
- Use nouns for concepts ("Authentication flow in API layer")
- Include context when helpful ("React components: Prefer composition over inheritance")

## nb todo vs nb tasks

Both `nb todo` and `nb tasks` can be used for tracking deferred work:
- Use whichever you prefer or are already using
- Both support adding, listing, and completing items
- Both support tags for organization
