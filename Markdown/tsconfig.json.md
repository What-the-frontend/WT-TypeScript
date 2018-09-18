tsconfig.json
===
Purpose of tsconfig.json file is manage compile options when you need compile typescript. If your typescript project has many compile options, you should use tsconfig.json file to easy compile. Use `tsc` command with many options is so complict. Now, Let's see how to write tsconfig.json file.

Write tsconfig.json
---
You can simply write tsconfig.json file by `tsc --init` command.
```javascript
{
  "compilerOptions": {
    /* Basic Options */
    "target": "es5",                          /* Specify ECMAScript target version: 'ES3' (default), 'ES5', 'ES2015', 'ES2016', 'ES2017','ES2018' or 'ESNEXT'. */
    "module": "commonjs",                     /* Specify module code generation: 'none', 'commonjs', 'amd', 'system', 'umd', 'es2015', or 'ESNext'. */
    // skip

    /* Strict Type-Checking Options */
    "strict": true,                           /* Enable all strict type-checking options. */
    // skip
    "esModuleInterop": true                   /* Enables emit interoperability between CommonJS and ES Modules via creation of namespace objects for all imports. Implies 'allowSyntheticDefaultImports'. */
    // skip
  }
}
```