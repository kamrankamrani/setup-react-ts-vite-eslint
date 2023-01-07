# Setup react + ts + vite + eslint + prettier

How to setup a react project with typescript, vite for bundling and eslint for debugging.

We use prettier with minimal setting for formatting code.

more about [Vite](https://vitejs.dev/guide/why.html)

## 1. first install vite and setup:

```
npm create vite@latest
```

### use the following settings: 

```
Project name: >> something

Select a framework: >> React

Select a variant: >> TypeScript
```

then move into your project:

```
cd my-project-name
```

## 2. Add prettier:

```
npm i -D prettier
```
create a `.prettierrc` file. put minimal configiration there:

```
{}
```

## 3. Add eslint:

```
npm i -D eslint
```

add the following file with name `.eslintrc`:

```
{}
```

We'll update it later.

## 4. Plugins:

#### Enable ESLint to support TypeScript:

```
npm install --save-dev @typescript-eslint/parser @typescript-eslint/eslint-plugin
```

#### Enable eslint to support prettier:

```
npm i -D eslint-config-prettier
```

#### Enable support linting of ES2015+ (ES6+) import/export syntax:

```
npm install eslint-plugin-import --save-dev
```

#### Enable typescript imports:

```
npm i -D eslint-import-resolver-typescript
```

#### Add eslint plugin for react:

```
npm i eslint-plugin-react --save-dev
```

#### ESLint plugin to enforce the Rules of Hooks:

```
npm install eslint-plugin-react-hooks --save-dev
```

## 5. Update `.eslintrc` file:

```
{
  "extends": [
    "eslint:recommended",
    "plugin:import/errors",
    "plugin:import/typescript",
    "plugin:react/recommended",
    "plugin:react/jsx-runtime",
    "plugin:react-hooks/recommended",
    "plugin:@typescript-eslint/recommended",
    "plugin:@typescript-eslint/recommended-requiring-type-checking",
    "plugin:@typescript-eslint/strict",
    "prettier"
  ],
  "plugins": ["react", "react-hooks", "import", "@typescript-eslint"],
  "parserOptions": {
    "ecmaVersion": 2022,
    "sourceType": "module",
    "project": ["./tsconfig.json"],
    "ecmaFeatures": {
      "jsx": true
    }
  },
  "rules": {
    "react/prop-types": 0,
    "react/react-in-jsx-scope": 0,
    "@typescript-eslint/no-empty-functions": 0,
    "import/no-unresolved": "error",
    "react/jsx-uses-vars": "error",
    "react-hooks/rules-of-hooks": "error",
    "react-hooks/exhaustive-deps": "warn"
  },
  "env": {
    "es6": true,
    "browser": true,
    "node": true
  },
  "settings": {
    "import/parsers": {
      "@typescript-eslint/parser": [".ts", ".tsx"]
    },
    "import/extensions": [".js", ".jsx", "ts", "tsx"],
    "import/resolver": {
      "node": {
        "extensions": [".js", ".jsx", ".ts", ".tsx"]
      },
      "typescript": {
        "typescript": {
          "alwaysTryTypes": true
        }
      }
    },
    // From here
    "react": {
      "createClass": "createReactClass", // Regex for Component Factory to use,
      // default to "createReactClass"
      "pragma": "React", // Pragma to use, default to "React"
      "fragment": "Fragment", // Fragment to use (may be a property of <pragma>), default to "Fragment"
      "version": "detect", // React version. "detect" automatically picks the version you have installed.
      // You can also use `16.0`, `16.3`, etc, if you want to override the detected value.
      // It will default to "latest" and warn if missing, and to "detect" in the future
      "flowVersion": "0.53" // Flow version
    },
    "propWrapperFunctions": [
      // The names of any function used to wrap propTypes, e.g. `forbidExtraProps`. If this isn't set, any propTypes wrapped in a function will be skipped.
      "forbidExtraProps",
      { "property": "freeze", "object": "Object" },
      { "property": "myFavoriteWrapper" },
      // for rules that check exact prop wrappers
      { "property": "forbidExtraProps", "exact": true }
    ],
    "componentWrapperFunctions": [
      // The name of any function used to wrap components, e.g. Mobx `observer` function. If this isn't set, components wrapped by these functions will be skipped.
      "observer", // `property`
      { "property": "styled" }, // `object` is optional
      { "property": "observer", "object": "Mobx" },
      { "property": "observer", "object": "<pragma>" } // sets `object` to whatever value `settings.react.pragma` is set to
    ],
    "formComponents": [
      // Components used as alternatives to <form> for forms, eg. <Form endpoint={ url } />
      "CustomForm",
      { "name": "Form", "formAttribute": "endpoint" }
    ],
    "linkComponents": [
      // Components used as alternatives to <a> for linking, eg. <Link to={ url } />
      "Hyperlink",
      { "name": "Link", "linkAttribute": "to" }
    ]
  }
}
```

*this is my recommended rules and plugins. you are free to choose your rules and plugins.*

## 6. Add the commands in `package.json`:

add following commands to run with npm:

```
"format": "prettier --write \"src/**/*.{js,jsx,ts,tsx}\"",
"lint": "eslint \"src/**/*.{js,jsx,ts,tsx}\" --quiet",
"typecheck": "tsc --noEmit"
```

then you can use `npm run lint` , `npm run typecheck` or `npm run format` easily.

## Here is my package.json look like:

```
{
  "name": "torch-switch",
  "private": true,
  "version": "0.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "tsc && vite build",
    "preview": "vite preview",
    "format": "prettier --write \"src/**/*.{js,jsx,ts,tsx}\"",
    "lint": "eslint \"src/**/*.{js,jsx,ts,tsx}\" --quiet",
    "typecheck": "tsc --noEmit"
  },
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0"
  },
  "devDependencies": {
    "@types/react": "^18.0.26",
    "@types/react-dom": "^18.0.9",
    "@typescript-eslint/eslint-plugin": "^5.48.0",
    "@typescript-eslint/parser": "^5.48.0",
    "@vitejs/plugin-react": "^3.0.0",
    "eslint": "^8.31.0",
    "eslint-config-prettier": "^8.6.0",
    "eslint-import-resolver-typescript": "^3.5.2",
    "eslint-plugin-import": "^2.26.0",
    "eslint-plugin-react": "^7.31.11",
    "eslint-plugin-react-hooks": "^4.6.0",
    "prettier": "^2.8.1",
    "typescript": "^4.9.3",
    "vite": "^4.0.0"
  }
}
```


### Contact:

```
k.kamranifard@gmail.com

@kamrankamrani73 --> Twitter
```





