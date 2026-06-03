# Team Blog

A [Quarto](https://quarto.org) + [Netlify](https://www.netlify.com) blog. Write a post, open a
Pull Request, review the live preview, then merge to publish. The repository holds only sources;
the site is built and deployed automatically by CI.

## Publish a post

1. Create a branch:
   ```bash
   git checkout -b post/my-topic
   ```

2. Create the post folder and file:
   ```bash
   mkdir -p posts/$(date +%Y-%m-%d)-my-topic
   $EDITOR posts/$(date +%Y-%m-%d)-my-topic/index.qmd
   ```
   A minimal `index.qmd`:
   ````markdown
   ---
   title: "My Post Title"
   author: "Your Name"
   date: "2026-06-03"
   categories: [R]
   ---

   Write your content here. You can embed executable code:

   ```{r}
   summary(cars)
   ```
   ````

3. (Optional) Preview locally:
   ```bash
   quarto preview
   ```

4. If your post uses an R package that is not installed in CI yet, add its name to the `pkgs`
   vector in `render.R`.

5. Commit, push, and open a Pull Request:
   ```bash
   git add -A
   git commit -m "Add post: My Post Title"
   git push -u origin post/my-topic
   gh pr create --fill        # or open the PR on GitHub
   ```

6. Wait for the green check, then click the **Preview** link the bot comments on the PR to see your
   post on a live, throwaway URL.

7. When the preview looks good, **merge the PR** — the production site updates automatically.

## Good to know

- Only sources go in git; the generated `_site/` is ignored.
- Each post lives in its own folder `posts/<date>-<slug>/index.qmd` with its own title, date, and
  categories.
- R/Python code blocks are executed during the build, and their output (text, tables, figures) is
  embedded in the published page.
