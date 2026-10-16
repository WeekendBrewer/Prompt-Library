# Briefcase: GitHub Pages prompt library

This is a static, read-only website backed by one CSV file. The 30 sample legal prompts live in `docs/prompts.csv`. The public interface is `docs/index.html`. A separate download, `private-prompt-editor.html`, is the editor; keep that file outside the published repository and open it locally on an editor's trusted computer.

## Publish the viewer

1. Create a GitHub repository and add this package's `docs/` folder and `README.md` to its default branch. Do **not** add `private-prompt-editor.html` to the repository or `docs/` folder. The ZIP supplied for the public site excludes the editor.
2. Open repository **Settings → Pages → Build and deployment**, choose **Deploy from a branch**, select the default branch and `/docs`, then save. The `.nojekyll` file in `docs/` keeps the site purely static. No build, server, or GitHub Action is required.
3. Use the Pages URL shown in Settings. For a project repository it is usually `https://OWNER.github.io/REPOSITORY/`.
4. The viewer fetches `./prompts.csv` from the same published folder on every page load and shows only entries whose `CatalogStatus` is not `Archived`. Search, categories, framework guidance, and copying a composed prompt work entirely in the reader's browser.

The Pages deployment may take time after a commit. A page refresh requests a new copy of the CSV. If the CSV fails to load, the viewer shows an error rather than substituting an old or hard-coded catalog.

## Use the separate editor

1. Give each designated editor a GitHub account with repository write access and a **fine-grained personal access token** restricted to this repository with **Contents: read and write**. If your organization requires token approval or SSO authorization, complete it in GitHub. Set an expiration. Never paste the token into a repository file, a shared document, or the viewer.
2. Download `private-prompt-editor.html` separately and open it locally in Chrome or another current browser. Enter `OWNER/REPOSITORY`, the publishing branch (typically `main`), CSV path `docs/prompts.csv`, and that editor's token. Choose **Load from GitHub**.
3. Add, edit, archive, or republish prompts. The editor suggests categories from keywords; selecting a category overrides that suggestion. The framework and optional professional role appear in the copied prompt. Editing first changes an in-memory working set.
4. Choose **Save CSV to GitHub** to commit the entire CSV to the same repository path the viewer fetches. The editor sends the current GitHub file SHA, so an intervening edit cannot silently overwrite the version it loaded. If there is a conflict, download the working CSV, reload, and reconcile changes before retrying.
5. **Download working CSV** makes a backup; **Replace working set from CSV** lets an editor update a local CSV in a spreadsheet and then publish it through the editor. Import requires all 11 CSV columns and unique `PromptKey` values. GitHub's commit history records earlier CSV versions.

The editor requests the token for the current browser session; it does not embed it, save it to local storage, or place it in the GitHub commit. Clear the token before leaving a shared computer. A locally opened file uses GitHub's browser-compatible REST API. If the browser or organization blocks local-file API calls, serve the editor only from an approved private internal origin, never the public Pages path.

## Access and publication

| Component | Who can access it | Who can change it |
| --- | --- | --- |
| GitHub Pages reader and `docs/prompts.csv` | Anyone who can reach the published Pages site | No editing controls in the viewer |
| GitHub repository | Determined by repository visibility and membership | Accounts with GitHub repository write permission |
| Local editor HTML | Only people to whom you separately give the file | Saving requires authorized GitHub credentials |

Keeping the editor HTML private is a distribution choice, not an authorization mechanism. GitHub checks the account and token on every write. The token authorizes repository Contents changes, not just this one CSV file. Choose your editors accordingly. A branch protection rule requiring a pull request may reject direct saves; use a branch configured to allow authorized CSV commits or publish reviewed changes through the GitHub interface.

GitHub Pages is **publicly accessible by default**, including when a repository is private. Do not publish confidential prompts, client facts, or internal work product unless your organization has configured and verified GitHub Enterprise Cloud private Pages access for its project site. An `Archived` CSV row remains in the published CSV and repository history, even though the viewer hides it. Remove sensitive material from the publishing source entirely.

## CSV columns

`PromptKey, Title, Summary, Category, CategoryMode, Framework, Jurisdiction, RolePerspective, Tags, PromptBody, CatalogStatus`

`CategoryMode` is `auto` or `manual`; `CatalogStatus` is `Published` or `Archived`. Preserve `PromptKey` when updating an entry. The legal prompt text is illustrative: a copied prompt asks the model to verify applicable primary authority, state uncertainty, and identify missing facts.

## Documentation

- [GitHub Pages branch and folder publishing](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)
- [GitHub REST API: repository contents](https://docs.github.com/en/rest/repos/contents)
- [GitHub REST API: CORS](https://docs.github.com/en/rest/using-the-rest-api/using-cors-and-jsonp-to-make-cross-origin-requests)
- [GitHub fine-grained personal access tokens](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)
- [Private GitHub Pages access](https://docs.github.com/en/enterprise-cloud@latest/pages/getting-started-with-github-pages/changing-the-visibility-of-your-github-pages-site)

Deployment status: the files and browser workflow have been checked locally. No repository has been created, no token has been issued, and no Pages site has been published for your account.
