# Notes from [Code Transformation and Linting with Abstract Syntax Trees](https://frontendmasters.com/courses/linting-asts)

## Abstract Syntax Trees

- AST is a concept to transform source code into data structures that are easy to work with for various static analysis tools,
  e.g. ESLint's [espree](https://github.com/eslint/espree)
- [AST visualizer](https://resources.jointjs.com/demos/rappid/apps/Ast/index.html)
- [AST Explorer](https://astexplorer.net/)
- [Esprima](https://github.com/eslint/espree)
- Parsers transform code into Syntax Trees, they might diffefrom one another due to different implementation goals
- Visitor pattern allows you to traverse the tree and perform some action on each node, e.g.

  ```javascript
  // ESLint example
  function create(context) {
    return {
      // This executes for every node with if statement
      IfStatement(node) {
        if (node.consequent.type !== "BlockStatement") {
          context.report({
            node,
            message: "Use blocks with if statements",
          });
        }
      },
    };
  }
  ```

- [Creating custom ESLint rules](https://eslint.org/docs/latest/extend/custom-rules)

## ESLint plugins

## Babel plugins

## Codemods
