
```dataviewjs
const tags = Object.keys(app.metadataCache.getTags())
  .filter(tag => tag.startsWith("#context/"))
  .sort();

const vault = app.vault.getName();

const links = tags.map(tag => {
  const label = tag.replace("#context/", "");
  const query = `task-todo:${tag}`;

  const url =
    `obsidian://search?vault=${encodeURIComponent(vault)}` +
    `&query=${encodeURIComponent(query)}`;

  return `[${label}](${url})`;
});

dv.list(links);

```