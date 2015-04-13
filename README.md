# gitignore-globs

Parse a `.gitignore` file into an array of glob patterns.

## Usage

.gitignore:

    node_modules
    package.json

index.js:

    var parse = require('gitignore-globs');

    var globs = parse('.gitignore');

    console.log(globs);
    // Result: ['node_modules', '**/node_modules/**', 'package.json']

## API

### parse([filepath<string>], [options<array>])

* filepath (string; default: `process.cwd() + '.gitignore'`) - Path to your `.gitignore`.
* options (array) - Options see below.

#### Options:

    {
        negate: false
    }

* negate (bool; default: false) - Option to negated patterns. Example: `package.json` => `!package.json`

## Rules

* Git: http://git-scm.com/docs/gitignore#_pattern_format
* Glob: https://github.com/isaacs/node-glob#glob-primer

**Mappings:**

| .gitignore | Description | Glob |
|------------|-------------|------|
| `#` | Comment | *ignore*
| ` ` | Blank line | *ignore*
| `/foo` | Ignore root (not sub) file and dir and its paths underneath. | `/foo`, `/foo/**`
| `/foo/` | Ignore root (not sub) foo dir and its paths underneath. | `/foo/**`
| `foo` | Ignore (root/sub) foo files and dirs and their paths underneath. | `foo`, `**/foo/**`
| `foo/` | Ignore (root/sub) foo dirs and their paths underneath. | `**/foo/**`

Other patterns already work as globs. For example:

* `*.zip`: Ignore any zip file.
* `.DS_Store`: Ignore all .DS_Store files.
* `*~`: Ignore all files that end with a tilde.
* `*.[oa]`: Ignore any files ending in ".o" or ".a", for example `archive.a` or `bar.o`.
* `*`: Ignore all files.

## Test

    npm test

### Watch:

    npm run watch-test

or

    nodemon --exec "mocha" test --exclude "node_modules"

## Resources

* .gitignore:
    * http://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository#Ignoring-Files
    * https://help.github.com/articles/ignoring-files/
    * http://git-scm.com/docs/gitignore#_pattern_format
    * https://www.npmjs.com/package/glob#glob-primer
* Others:
    * https://github.com/EE/gitignore-to-glob
    * https://github.com/jonschlinkert/parse-gitignore
    * https://github.com/codemix/gitignore-parser
    * https://github.com/jenseng/globby-js

## License

MIT © Bernhard Wanger, [Sevenweb](https://sevenweb.com)
