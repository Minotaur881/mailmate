# update README + ncu@0637d80

[Permalink](update-readme-+-ncu-0637d80.md)

 Showing with **231 additions** and **1,917 deletions**.

1.  +2 −2 [README.md](update-readme-+-ncu-0637d80.md#diff-b335630551682c19a781afebcf4d07bf978fb1f8ac04c6bf87428ed5106870f5)
2.  +217 −1,904 [package-lock.json](update-readme-+-ncu-0637d80.md#diff-053150b640a7ce75eff69d1a22cae7f0f94ad64ce9a855db544dda0929316519)
3.  +11 −11 [package.json](update-readme-+-ncu-0637d80.md#diff-7ae45ad102eab3b6d7e7896acd08c427a9b25b346470d7bc6507b6481575d519)
4.  +1 −0 [tsconfig.json](update-readme-+-ncu-0637d80.md#diff-b55cdbef4907b7045f32cc5360d48d262cca5f94062e353089f189f4460039e0)

|  |  | @@ -1,7 +1,7 @@ |
| :--- | :--- | :--- |
|  |  |  1. make sure you have node installed |
|  |  |  2. run \`npm install\` |
|  |  |  3. install BBT in Zotero. Right-click a collection or library and select "Show BibLaTeX server URL". |
|  |  |  4. edit \`config.json\`. Paste the URL from step 3 into the field \`collection\` but change \`.biblatex\` into \`.csljson\`. Also paste the URL in your browser so you can see what the objects look like |
|  |  |  3. install BBT in Zotero. Right-click a collection or library and select "Download Better BibTeX export", and choose the "CSL JSON" format. |
|  |  |  4. edit \`config.json\`. Paste the URL from step 3 into the field \`collection\`. Also paste the URL in your browser so you can see what the objects look like |
|  |  |  5. edit \`template.html\`. The template understands \[nunjucks\]\(https://mozilla.github.io/nunjucks/\) syntax; the objects it inserts are in CSL-JSON format, the fields of which are documented \[here\]\(https://docs.citationstyles.org/en/stable/specification.html\#appendix-iv-variables\). Variables with dashes \(\`-\`\) are available in camelCase in the template, so a variable like \`container-title\` is \`containerTitle\` in the template. |
|  |  |  6. create a directory called \`output\` if it doesn't exist, or add a field called \`output\` to \`config.json\` pointing to the output directory |
|  |  |  7. run \`npm start\` |
|  |  |  |

