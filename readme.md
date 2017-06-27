# bash-ast-traverser

> Traverse an AST object created by `bash-parser`

# Usage

```js
const traverse = require('bash-ast-traverser');
traverse(ast, {
	Command(node) {
		If (node.name.text !== '') {
			const expectAliasCheck =
				node.name.maybeSimpleCommandName ||
				node.name.text.indexOf('$') !== -1 ||
				node.name.text[0].match(/[0-9]/);

			assert.ok(expectAliasCheck, `expected Command name ${JSON.stringify(node, null, 2)}`);
		}
		delete node.name.maybeSimpleCommandName;
	},

	defaultMethod(node) {
		assert.ok(!node.maybeSimpleCommandName, `Command name not expected ${JSON.stringify(node, null, 2)}`);
		delete node.maybeSimpleCommandName;
	}
});
```



[![Travis Build Status](https://img.shields.io/travis/vorpaljs/bash-ast-traverser/master.svg)](http://travis-ci.org/vorpaljs/bash-ast-traverser)
[![NPM module](https://img.shields.io/npm/v/bash-ast-traverser.svg)](https://npmjs.org/package/bash-ast-traverser)
[![NPM downloads](https://img.shields.io/npm/dt/bash-ast-traverser.svg)](https://npmjs.org/package/bash-ast-traverser)


# License

The MIT License (MIT)

Copyright (c) 2017 vorpaljs
