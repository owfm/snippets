```typescript
jest.mock("./my-module", () => {
  const original = jest.requireActual("./my-module");
  return {
    __esModule: true,
    ...original, // module's other functions and exports
    methodThatIwantToMock: jest.fn(() => [
      {
        key1: "mock data",
        key2: "more mock data",
      },
    ]),
  };
});
```
