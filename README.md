# Briefcase: GitHub Pages prompt library

The public, read-only website is in `docs/index.html`. Its only data file is `docs/prompts.csv`, which contains 30 sample legal prompts. A separate download, `private-prompt-editor.html`, lets designated editors work locally. Keep that HTML file outside the public repository.

## Publish the viewer

1. Extract the ZIP before uploading anything. Its files belong at the **repository root**: `README.md`, `docs/index.html`, `docs/prompts.csv`, and `docs/.nojekyll`. In GitHub's file browser, `REPOSITORY/tree/BRANCH/docs` should show `index.html` and `prompts.csv` directly. Do not upload the ZIP itself, and do not place `docs` inside another folder. The public-site ZIP excludes the editor HTML.
2. In repository **Settings → Pages → Build and deployment**, choose **Deploy from a branch**, then select the branch containing those files (often `main`) and `/docs`. Confirm that `docs/.nojekyll` exists in the repository. Create that empty file in `docs/` if a browser upload omitted it. It prevents Jekyll from processing this static site.
3. Open the Pages URL shown in settings. The viewer reads `./prompts.csv` when the page loads, shows published prompts, and offers search, categories, framework guidance, and copy controls.

## Update prompts without a token or API setup

1. In GitHub, open `docs/prompts.csv` and download the current file. Use the latest repository version whenever starting an editing session.
2. Open the separately supplied `private-prompt-editor.html` on a trusted computer. Select **Open prompts.csv** and choose the downloaded CSV.
3. Add or edit prompts, select a category manually when the automatic suggestion is unsuitable, and archive or republish entries as needed. Select **Download revised prompts.csv** when finished.
4. Confirm the downloaded filename is exactly `prompts.csv`. In the GitHub repository's `docs/` folder, upload that file to replace `docs/prompts.csv` and commit the change. Only users with repository write permission can commit the replacement. Refresh the published page after GitHub Pages completes its update.

Before committing, review GitHub's changed-file diff to ensure another editor's intervening changes have not been lost. A direct file replacement has no automatic conflict detection. GitHub's commit history provides earlier versions if a restoration is needed. If branch protection prevents a direct commit, publish through your organization's review workflow instead.

The editor requires all 11 CSV columns and unique `PromptKey` values. Editing a prompt preserves its key. A CSV load replaces the editor's entire in-memory working set, and an unsaved-change warning appears before discarding modifications. The editor does not make any network requests or hold a GitHub token.

## Access and publication

| Component | Reader access | Write access |
| --- | --- | --- |
| GitHub Pages site and published CSV | Anyone who can access the Pages site | None through the site |
| GitHub repository | According to repository visibility | Designated accounts with repository write permission |
| Separate local editor HTML | People to whom you supply the editor file | Can prepare a CSV; a repository writer must commit it |

Keeping the editor file private does not authorize editing the repository. GitHub permissions control commits. GitHub Pages is publicly accessible by default, even for many private repositories. GitHub Enterprise Cloud can provide private Pages access for qualifying organizational project sites. Verify the site's visibility before publishing any internal or confidential material.

Archived rows are still present in `docs/prompts.csv` and repository history, although hidden in the viewer. Do not use `Archived` for confidential drafts. The sample prompts are illustrations; each copied prompt asks counsel to check applicable law and source material.

## CSV fields

`PromptKey, Title, Summary, Category, CategoryMode, Framework, Jurisdiction, RolePerspective, Tags, PromptBody, CatalogStatus`

`CategoryMode`: `auto` or `manual`. `CatalogStatus`: `Published` or `Archived`. Preserve each existing `PromptKey`. Leasing and land use are separate categories. The framework and optional professional role are included when copying a prompt.

## References

- [Configure GitHub Pages from a branch](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)
- [Upload files to a GitHub repository](https://docs.github.com/en/repositories/working-with-files/managing-files/adding-a-file-to-a-repository)
- [Edit files and review GitHub changes](https://docs.github.com/en/repositories/working-with-files/managing-files/editing-files)
- [Private Pages access](https://docs.github.com/en/enterprise-cloud@latest/pages/getting-started-with-github-pages/changing-the-visibility-of-your-github-pages-site)

Deployment status: this package is ready for your repository. No GitHub repository or Pages site has been created in your account.
