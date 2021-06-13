# retorquere/devonthink

 28 lines \(28 sloc\) 730 Bytes

|  | { |
| :--- | :--- |
|  |  "name": "zotero-devonthink", |
|  |  "version": "1.0.19", |
|  |  "description": "Copies the contents of a Zotero collection to HTML files for import into DevonThink", |
|  |  "scripts": { |
|  |  "prestart": "npm install", |
|  |  "start": "ts-node index.ts", |
|  |  "test": "tslint -t stylish --project .", |
|  |  "postversion": "git push --follow-tags" |
|  |  }, |
|  |  "author": "Emiliano Heyns", |
|  |  "license": "ISC", |
|  |  "dependencies": { |
|  |  "@types/node": "^13.11.1", |
|  |  "alert-node": "^3.0.11", |
|  |  "commander": "^5.0.0", |
|  |  "mkdirp": "^1.0.4", |
|  |  "nunjucks": "^3.2.1", |
|  |  "request": "^2.88.2", |
|  |  "request-promise": "^4.2.5", |
|  |  "slug": "^2.1.1", |
|  |  "ts-node": "^8.8.2", |
|  |  "typescript": "^3.8.3" |
|  |  }, |
|  |  "devDependencies": { |
|  |  "tslint": "^6.1.1" |
|  |  } |
|  | } |

*  Copy lines
*  Copy permalink
* [View git blame](https://github.com/retorquere/devonthink/blame/0637d807752287880e8c2b9b8afd740f77ca2596/package.json)
* [Reference in new issue](https://github.com/retorquere/devonthink/issues/new)

