## Markdown basics

### Headings

To create a heading, use a hash mark (#)

```markdown
# This is heading 1
## This is heading 2
### This is heading 3
#### This is heading 4
```

### Bold and italic text

To format text as bold, enclose it in two asterisks

```markdown
This text is **bold**.
```

To format text as italic, enclose it in single asterisk

```markdown
This text is *italic*.
```

### Lists

To format an ordered list, use corresponding numbers.

```markdown
1. First item
1. Second item
1. Thrid item
```

To format an unordered list, use dashes

```markdown
- Item 1
- Item 2
- Item 3
```

### Tables

Tables are not part of the core Markdown specification, but GFM supports them. You can create tables by using the pipe (|) and hyphen (-) characters. Hyphens create each column's header, while pipes separate each column. Include a blank line before your table so it's rendered correctly.

```markdown
| Fun                  | With                 | Tables          |
| :------------------- | -------------------: |:---------------:|
| left-aligned column  | right-aligned column | centered column |
| $100                 | $100                 | $100            |
| $10                  | $10                  | $10             |
| $1                   | $1                   | $1              |
```

### Links

```markdown
[link text](file path)
```

### Code

To use inline code, use a single backtick (`)

```markdown
Welcome to `hello world` section.
```

To use code block, use triple backticks (```)

```markdown
​```csharp
public static void Main(string[] args)
{
    Console.Writeline("Hello World!");
}
​```
```
15 18