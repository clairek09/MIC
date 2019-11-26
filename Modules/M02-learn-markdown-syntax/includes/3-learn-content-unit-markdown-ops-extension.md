## OPS custom Markdown extensions

### Alerts (Note, Tip, Important, Caution, Warning)

In learn, the note blocks are support

```markdown
> [!NOTE]
> Information the user should notice even if skimming.

> [!TIP]
> Optional information to help a user be more successful.

> [!IMPORTANT]
> Essential information required for user success.

> [!CAUTION]
> Negative potential consequences of an action.

> [!WARNING]
> Dangerous certain consequences of an action.
```

### Section definition for code

```markdown
> [!div class="tabbedCodeSnippets" data-resources="OutlookServices.Calendar"]
> ```cs
> <cs code text>
> ```
> ```javascript
> <js code text>
> 
```

### Single selector and Multi-selector



### Checklist

```markdown
> [!div class="checklist"]
> * List item 1
> * List item 2
> * List item 3
```

### Table Wrapping

**mx-tdBreakAll**

If you create a table in Markdown, the table might expand to the right navigation and become unreadable. You can solve that by allowing Docs rendering to break the table when needed. Just wrap up the table with the custom class `[!div class="mx-tdBreakAll"]`.

```markdown
> [!div class="mx-tdBreakAll"]
> |Name|Syntax|Mandatory for silent installation?|Description|
> |-------------|----------|---------|---------|
> |Quiet|/quiet|Yes|Runs the installer, displaying no UI and no prompts.|
> |NoRestart|/norestart|No|Suppresses any attempts to restart. By default, the UI will prompt before restart.|
> |Help|/help|No|Provides help and quick reference. Displays the correct use of the setup command, including a list of all options and behaviors.|
```

### Video

[Upload videos to RedTiger](https://www.redtigerwiki.com/wiki/Digital_Asset_Manager_Overview)

```markdown
> [!VIDEO <video_url_from_redtiger>]
```

**Sample 1,**
```markdown
> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RWtXMf]
```

### video test
video 1
> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RWtXMf]

video 2:
> [!VIDEO What is a Computer.mp4]

### Code

In learn, the snippet is supported

```markdown
[!code-<language>[<name>](<codepath><queryoption><queryoptionvalue> "<title>")]
```

For example:

```markdown
[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-docker-host/create-docker-host.sh?range=13-18&highlight=2,5 "Docker Host")
```

### Includes other markdown

```markdown
[!INCLUDE [notes](../notes.md)]
```

### Knowledge Checks

[how to write knowledge checks](https://review.docs.microsoft.com/en-us/learn-docs/docs/id-guidance-knowledge-check?branch=master) for Learn

```markdown
- content: "What needs to be installed on your machine to let you execute Azure PowerShell cmdlets locally?"

    choices:

    - content: "The Azure cloud shell"

      isCorrect: false

      explanation: "The cloud shell does let you execute Azure cmdlets; however, you use it in a browser, so you are not running the commands on your local machine."

    - content: "The base PowerShell product and the AzureRM module"

      isCorrect: true

      expalanation: "You need both the base PowerShell product and the AzureRM module. The base product gives you the shell itself, a few core commands, and programming constructs like loops, variables, etc. The AzureRM modules adds the cmdlets you need to work with Azure resources."

    - content: "The Azure CLI and Azure PowerShell"

      isCorrect: false

      explanation: "The Azure CLI is an alternate command-line and scripting tool. It is not needed if you are going to use Azure PowerShell."
```