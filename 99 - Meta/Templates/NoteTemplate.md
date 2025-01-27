<%* 
// Prompt the user for a title to append
let userTitle = await tp.system.prompt("Enter title");

// Get the current file title (this assumes it should start with a UNIX timestamp)
let currentTitle = tp.file.title;

// If the title doesn't contain a UNIX timestamp, add one
if (!currentTitle.match(/^\d+/)) {
    let unixTimestamp = Math.floor(Date.now() / 1000);  // Get current UNIX timestamp
    currentTitle = `${unixTimestamp} - ${currentTitle}`;  // Prepend timestamp to current title
}

// Construct the new title
let newTitle = userTitle ? `${currentTitle.split(' - ')[0]} - ${userTitle}` : `${currentTitle.split(' - ')[0]} - Untitled Suffix`;

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
