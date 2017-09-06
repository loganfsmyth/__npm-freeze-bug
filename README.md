## Reproduction repo for an infinite loop in npm 5.x

To reproduce

```
cd babel-plugin-transform-es2015-modules-commonjs
npm link
```

There are a few different messages it locks up on, depending on what seems to vary. The most common one being

> npm linkTree:loadAllDepsIntoIdealTree: sill install loadIdealTree

It would appear that npm's in-memory tree structure is either corrupted, or incorrect assumptions are made somewhere. It's locking up in this loop

https://github.com/npm/npm/blob/2091dd1c748e54e85e904ce8da3b3975ee99117d/lib/install/deps.js#L563

because a node appears to be its own parent.
