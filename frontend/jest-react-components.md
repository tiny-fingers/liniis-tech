# Configure Jest (jsdom)

Dependencies:

```bash
npm install --save-dev jest
```

## With Typescript

```bash
npm install --save-dev ts-jest
```

### Common transformer

I often have projects with `.svg` files, which Jest cannot transform out-of-the-box.

```bash
npm in install --save-dev jest-transformer-svg
```

Then configure jest to use the transformer

## Jest config

Using *jest.config.mjs* instead of *jest.config.js* allows us to writing import and export syntax of ECMAScript Modules (ESM) instead of CommonJs pattern such as *require* and *module.export*  

```js
// jest.config.mjs
export default {
  testEnvironment: 'jsdom', // use this to test react compoentns, otherwise 'node' 
  preset: 'ts-jest', // working with Typescript

  extensionsToTreatAsEsm: ['.ts', '.tsx'],
  transform: {
    '^.+\\.(js|jsx)$': 'babel-jest', // use babel con transpile node_modules dependencies written in EMS
    "^.+\\.svg$": "jest-transformer-svg", // transform .svg file
    '^.+\\.(ts|tsx)$': ['ts-jest', {
      useESM: true, // work with modules exports with ESM syntax
    }]
  },
  moduleFileExtensions: ['ts', 'tsx', 'js', 'jsx', 'json'],
  transformIgnorePatterns: [
    '\\.(css|scss|sass)$', // help jest load *.css filess
    'node_modules/(?!(d3-[^/]+|internmap|date-fns)/)'], // do not tranform modules d3-*, internmap, etc.

  moduleNameMapper: {
    '\\.(css|less|scss|sass)$': 'identity-obj-proxy',
    '\\.module\\.(css|scss|sass)$': 'identity-obj-proxy',

    '^@/(.*)$': '<rootDir>/src/$1',
    '^@hooks$': '<rootDir>/src/hooks',
  },
  testMatch: [
    '<rootDir>/src/**/__tests__/**/*.(ts|tsx|js|jsx)',
    '<rootDir>/src/**/?(*.)+(test|spec).(ts|tsx|js|jsx)'
  ],

  setupFilesAfterEnv: ['<rootDir>/setupTests.ts'],

  collectCoverageFrom: [
    'src/**/*.{ts,tsx}',
    '!src/**/*.d.ts',
    '!src/index.tsx'
  ]
};

```

## Links

- configure jest for node: [Configure Jest (node)](/jest-node.md)
