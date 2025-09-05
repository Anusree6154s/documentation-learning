## Testing with mocha

### Why we need tests
- Manual checking is unreliable: fixing one case may break another.  
- Automated tests check all cases every time.  
- Prevents regressions and missed errors.  

<br>

### Behavior Driven Development (BDD)
- Combines **tests, documentation, and examples**.  
- Specs describe expected behavior before implementation.  

<br>

### Mocha + Chai + Sinon
- **Mocha** → testing framework (`describe`, `it`, `mocha.run`).  
- **Chai** → assertions (`assert.equal`, `assert.isNaN`, etc.).  
- **Sinon** → spies/mocks (used later).  

<br>

### Example: `pow(x, n)`
1. Write spec first:  
   ```js
   describe("pow", function() {
     it("raises to n-th power", function() {
       assert.equal(pow(2, 3), 8);
     });
   });
   ```
2. Implement step by step → tests guide correctness.  
3. Add more tests (different inputs).  
4. Fix implementation until all tests pass.  

<br>

### Best practices
- **One test = one check** (split asserts into separate `it`).  
- Use **nested describe** to group related tests.  
- `before/after`, `beforeEach/afterEach` → setup and cleanup.  

<br>

### Example enhancements
- Use loops to generate multiple tests.  
- Add edge cases (negative `n`, non-integer `n`).  
- Example assertion:  
  ```js
  assert.isNaN(pow(2, -1));
  assert.isNaN(pow(2, 1.5));
  ```

<br>

### Benefits of automated tests
- Safer changes and refactoring.  
- Faster feedback, fewer bugs.  
- Improves architecture (clear inputs/outputs).  
- Encourages iterative development.  

<br>

⚡ **Summary:**  
Write specs → implement → run tests → refine. Tests act as **safety net, documentation, and usage examples** all at once.  
