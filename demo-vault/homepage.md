# today

```tasks
not done
path does not include templates
tags include #today
```

# contexts

[[contexts]]
# action

```tasks
not done
path does not include templates
tags include #action
tags does not include #today
```

# projects

```tasks
tags include #project 
not done
```

## project folders & notes

dataview js...

```dataviewjs
const path = "1_Projects";

const folder = app.vault.getAbstractFileByPath(path);

if (!folder?.children) {
    dv.paragraph(`Folder not found: ${path}`);
} else {
    const items = folder.children
        .filter(x =>
            x.children ||                         // folders
            x.extension?.toLowerCase() === "md"   // markdown files
        )
        .sort((a, b) =>
            a.name.localeCompare(b.name, undefined, {
                sensitivity: "base"
            })
        );

    const ul = dv.el("ul", "");

    for (const x of items) {
        const li = ul.createEl("li");

        if (x.children) {
            const a = li.createEl("a", {
                text: `${x.name} 📁`,
                cls: "internal-link"
            });

            a.addEventListener("click", async (e) => {
                e.preventDefault();

                const fileExplorer = app.workspace.getLeavesOfType("file-explorer")[0];
                if (fileExplorer?.view?.revealInFolder) {
                    await fileExplorer.view.revealInFolder(x);
                }
            });
        } else {
            const a = li.createEl("a", {
                text: x.basename,
                cls: "internal-link"
            });

            a.addEventListener("click", async (e) => {
                e.preventDefault();
                await app.workspace.getLeaf(false).openFile(x);
            });
        }
    }
}
```


# inbox

```tasks
not done
path does not include templates
tags does not include #action
```


