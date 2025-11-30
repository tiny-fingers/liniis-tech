# Configure Jest (node)

Dependencies:

```bash
npm install --save-dev jest
```

## With Typescript

```bash
npm install --save-dev ts-jest
```

## Jest config

By default, jest is configured to use CommonJs.

```js
// jest.config.js
module.exports = {
  preset: 'ts-jest',
  testEnvironment: 'node',
  roots: ['<rootDir>/src'],
  testMatch: [
    '**/__tests__/**/*.+(ts|tsx|js)',
    '**/*.(test|spec).+(ts|tsx|js)',
  ],
  transform: {
    '^.+\\.(ts|tsx)$': 'ts-jest',
  },
  collectCoverageFrom: [
    'src/**/*.{ts,tsx}',
    '!src/**/*.d.ts',
    '!src/index.tsx',
  ],
  moduleFileExtensions: ['ts', 'tsx', 'js'],
};

```
