# bash-ast-traverser

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



[![Travis Build Status](https://img.shields.io/travis/vorpaljs/mode-grammar-builder/master.svg)](http://travis-ci.org/vorpaljs/mode-grammar-builder)
[![NPM module](https://img.shields.io/npm/v/mode-grammar-builder.svg)](https://npmjs.org/package/mode-grammar-builder)
[![NPM downloads](https://img.shields.io/npm/dt/mode-grammar-builder.svg)](https://npmjs.org/package/mode-grammar-builder)


# License

The MIT License (MIT)

Copyright (c) 2017 vorpaljs
