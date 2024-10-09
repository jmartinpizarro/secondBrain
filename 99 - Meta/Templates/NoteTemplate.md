<%* 
// Prompt the user for a title to append
let userTitle = await tp.system.prompt("Enter title");
// Get the current file title
let currentTitle = tp.file.title;
// Append the user's input to the current title
let newTitle = userTitle ? `${currentTitle} ${userTitle}` : `${currentTitle} - Untitled Suffix`;
// Rename the file
await tp.file.rename(newTitle);
-%>
---
aliases:
  - <% userTitle %>
tags:
  - review
"References":
cssclasses:
---
# <% userTitle %>
<% tp.file.cursor(10) %>

***