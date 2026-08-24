---
name: repo-fact
description: Use when a prompt asks for the facts of this repository. Read the MOTTO file and count the markdown files, then report both.
---

# repo-fact

Do these steps inside the current working directory:

1. Read the file `MOTTO` and take its one line as the motto.
2. Count the files whose name ends in `.md`, at the top level only.
3. Give the motto and the count as the facts.

Keep any reply format the prompt asks for.
