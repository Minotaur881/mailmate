# Refactor and add tests for better maintainability@bee41ec

 @@ -1,32 +1,74 @@ \#\# Install \# Github Repos workflow for Alfred  
 Download from \[packal\]\(http://www.packal.org/workflow/github-repos-0\) to keep it up to date.  
 You can also check the \[releases history\]\(https://github.com/edgarjs/alfred-github-repos/releases\).  
 --- This is a custom workflow for the \[Alfred app\]\[alfred-app\] that lets you search and open a Github repository via the Github Search API.  
 \#\# Authentication  
 1. Call \`gh-token\` to generate personal access token. 2. Login by calling the \`gh-login\` action. You'll need to authenticate with a personal access token that you can generate in the \[Github developer settings page\]\[personal-access-token\] or by running the \`gh-token\` command in Alfred.  
 After you have copied your personal access token, run \`gh-login\` to set your personal access token.  
 \#\# Usage  
 1. Search your repositories by calling the \`gh\` action. 2. Search all repositories by calling the \`gha\` action. 3. Your repositories are cached. To force re-download cache use \`gh-reset-cache\` action or choose corresponding item in the \`gh\` action. Here's the list of available commands.  
 \#\#\# Global Search: \`gh\`  
 The example above will search for repositories with the string "hello-world" in their name. Internally this uses the \[Github Search syntax\]\[github-search\], so you can use modifiers like:  
 gh hello-world stars:&gt;100  
 This will search only in repositories that have more than 100 stars.  
 &gt; Please note that this command only searches in the repository name. This means that your query will be appended with the \`in:name\` modifier. So when you type in \`hello-world\`, the final search query sent will be: "hello-world in:name". \#\#\# Search your repositories: \`repo \[query\]\`  
 This command works the same as the previous one \(\`gh\`\) but it limits the search to your own repositories.  
 \#\#\# Other Actions &gt; This includes repositories from your organizations as well. \* \`gh-notifications\` will open your Github notifications page. \#\#\# Search Pull Requests: \`pr \[query\]\`  
 This command searches within the Pull Requests that you're involved in.  
 \#\#\# Open notifications: \`gh-notifications\`  
 This command just opens your \[Github notification\]\[notifications-page\] page.  
 \#\# Configuring host for Enterprise  
 If you're using an Enterprise account, you can call the \`gh-host\` command.  
 ---  
 \#\#\# Enterprise Support \#\# Contributing  
 You can submit your bug reports or feature requests at: https://github.com/edgarjs/alfred-github-repos/issues  
 If you want to submit a Pull Request, please follow these simple guides:  
 1. Add a detailed description of what you're changing and why. 2. Add necessary unit tests that cover your changes. 3. Don't increase the version of the workflow in your changes.  
 Here are some ideas for Pull Requests:  
 - \[ \] Make search faster - \[ \] Search commits in a repository - \[ \] Search projects in an organization - \[ \] Improve icon graphics  
 If you're using an enterprise account, set your enterprise host with \`gh-host\`. \#\# License  
 The host value should be something like \`https://example.com\` This project is published under the \[MIT License\]\(LICENSE.md\).  
 NOTE: This is an experimental feature that may not work as expected, if you find any issues please report them here: https://github.com/edgarjs/alfred-github-repos/issues \[alfred-app\]: https://www.alfredapp.com/ \[github-search\]: https://docs.github.com/en/free-pro-team@latest/github/searching-for-information-on-github/searching-on-github \[download-packal\]: https://www.packal.org/workflow/github-repos \[download-releases\]: https://github.com/edgarjs/alfred-github-repos/releases \[personal-access-token\]: https://github.com/settings/tokens/new?description=Github%20Repos%20Alfred%20workflow&scopes=repo \[pulls-page\]: https://github.com/pulls \[notifications-page\]: https://github.com/notifications \[alfred-env-vars\]: https://www.alfredapp.com/help/workflows/script-environment-variables/

