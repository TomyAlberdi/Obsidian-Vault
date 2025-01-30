Created: 2024-09-22 18:32
## Family Tree:
1. Computer
2. Frontend Development
3. [[React]]
-- -
A **hook** is a special function that allows you to connect to React's features. Hooks are essentially functions that enable functional components to incorporate React features, which were previously only available to class components. Among other utilities, they provide functional components with internal state and lifecycle methods.
Additionally, they allow for:
- Better and simplified code reuse, composition, and testing.
- Extracting logic from a component for reuse and sharing.
**Benefits**:
- Less code.
- More organized code.
- Use of reusable functions.
- Easier testing.
- No need to call `super()` in a class constructor.
- No dealing with JavaScript's `this` and `bind`.
- Local state is within the scope of handlers and side-effect functions.
- Smaller components that make React's job easier.
**Rules for hooks**:
- Do not call hooks inside conditionals, loops, or nested functions.
- Only call hooks inside React functional components.
- Call hooks at the beginning of the component function.