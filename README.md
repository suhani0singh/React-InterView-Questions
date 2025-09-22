# 📝 Top React Interview Questions

## 1. React Basics (1–20)

1. What is React?
	 <details>
	 <summary>Answer</summary>
   
	 - React is a JavaScript library for building user interfaces using a component-based, declarative approach.
	 - You describe what the UI should look like for a given state, and React efficiently updates the DOM when state changes.
   
	 Real‑world example: A product card on an e‑commerce site that can be reused across the homepage, category pages, and the cart.
   
	 ```jsx
	 // ProductCard.jsx
	 export default function ProductCard({ product, onAddToCart }) {
		 return (
			 <article className="card">
				 <img src={product.image} alt={product.title} />
				 <h3>{product.title}</h3>
				 <p>${product.price}</p>
				 <button onClick={() => onAddToCart(product)}>Add</button>
			 </article>
		 );
	 }
	 ```
   
	 Diagram (component composition):
   
	 ```mermaid
	 graph TD
		 App --> Header
		 App --> ProductList
		 ProductList --> ProductCard
	 ```
	 </details>
   
2. What are the main features of React?
	 <details>
	 <summary>Answer</summary>
   
	 - Component-based UI
	 - Declarative rendering with JSX
	 - Virtual DOM and efficient reconciliation
	 - One-way data flow (props down, events up)
	 - Hooks for state and side effects in function components
   
	 Example: A search box component that manages its input state and emits changes upward.
   
	 ```jsx
	 function SearchBox({ onChange }) {
		 const [q, setQ] = React.useState("");
		 return (
			 <input
				 value={q}
				 placeholder="Search products"
				 onChange={(e) => {
					 setQ(e.target.value);
					 onChange(e.target.value);
				 }}
			 />
		 );
	 }
	 ```
   
	 ```mermaid
	 flowchart LR
		 State[Component State] --> View
		 View -->|User Events| Handler
		 Handler -->|setState| State
	 ```
	 </details>
   
3. What are the advantages of using React?
	 <details>
	 <summary>Answer</summary>
   
	 - Performance via Virtual DOM and batching
	 - Reusability and composition of components
	 - Huge ecosystem (libraries, tooling, community)
	 - Cross-platform via React Native
	 - Strong developer experience (Hooks, DevTools)
   
	 Example: Reusing the same `Button` component across 10 pages keeps behavior and styles consistent and reduces bugs.
   
	 ```jsx
	 export function Button({ variant = "primary", ...props }) {
		 return <button className={`btn btn-${variant}`} {...props} />;
	 }
	 ```
	 </details>
   
4. What are the limitations of React?
	 <details>
	 <summary>Answer</summary>
   
	 - Just the view layer: you must choose routing, state mgmt, data fetching, etc.
	 - Many choices can mean decision overhead for teams
	 - SEO for SPAs requires SSR/SSG or hydration (Next.js)
	 - Bundle size if not careful with code splitting
   
	 Example: A content-heavy marketing site might be simpler and faster to build with static site generators than a full SPA.
	 </details>
   
5. What is JSX?
	 <details>
	 <summary>Answer</summary>
   
	 - JSX is a syntax extension that lets you write XML-like markup inside JavaScript to describe UI structure.
	 - It compiles to `React.createElement(...)` calls.
   
	 ```jsx
	 const title = <h1>Welcome</h1>; // JSX
	 // Compiles roughly to:
	 // React.createElement('h1', null, 'Welcome')
	 ```
	 </details>
   
6. Why can’t browsers read JSX directly?
	 <details>
	 <summary>Answer</summary>
   
	 - Browsers understand JavaScript, not JSX. JSX must be transpiled (e.g., by Babel) into standard JS before execution.
   
	 ```jsx
	 // JSX (source)
	 const node = <Button disabled={isBusy}>Pay</Button>;
   
	 // Transpiled output (conceptually)
	 const node = React.createElement(Button, { disabled: isBusy }, 'Pay');
	 ```
	 </details>
   
7. What is the difference between React and Angular/Vue?
	 <details>
	 <summary>Answer</summary>
   
	 - React: library focused on view; choose your own routing, state, data; JSX; unidirectional data flow.
	 - Angular: full framework; TypeScript-first; DI, RxJS, CLI baked in; templates.
	 - Vue: progressive framework; SFCs (`.vue`), reactivity system, directives, built-in router/state libs.
   
	 Real‑world consideration: If you want maximum flexibility and a massive ecosystem, React is great. If you prefer batteries-included conventions, Angular may fit better; Vue sits between.
	 </details>
   
8. What are components in React?
	 <details>
	 <summary>Answer</summary>
   
	 - Components are reusable, isolated pieces of UI that accept inputs (props) and return elements.
	 - Components compose to form complex interfaces.
   
	 ```jsx
	 function Header() { return <header>Shop</header>; }
	 function Layout({ children }) {
		 return (<>
			 <Header />
			 <main>{children}</main>
		 </>);
	 }
	 ```
	 </details>
   
9. What are functional components?
	 <details>
	 <summary>Answer</summary>
   
	 - Plain JavaScript functions that return JSX; they can use Hooks for state and side effects.
   
	 ```jsx
	 function Counter() {
		 const [count, setCount] = React.useState(0);
		 return (
			 <div>
				 <p>Count: {count}</p>
				 <button onClick={() => setCount(c => c + 1)}>+1</button>
			 </div>
		 );
	 }
	 ```
	 </details>
   
10. What are class components?
	 <details>
	 <summary>Answer</summary>
   
	 - ES6 classes that extend `React.Component` and use lifecycle methods. Less common in new code since Hooks.
   
	 ```jsx
	 class Clock extends React.Component {
		 state = { time: new Date() };
		 componentDidMount() { this.t = setInterval(() => this.setState({ time: new Date() }), 1000); }
		 componentWillUnmount() { clearInterval(this.t); }
		 render() { return <span>{this.state.time.toLocaleTimeString()}</span>; }
	 }
	 ```
	 </details>
   
11. What are props in React?
	 <details>
	 <summary>Answer</summary>
   
	 - Read-only inputs to a component. Parent passes props; child renders based on them and can raise events back.
   
	 ```jsx
	 function Avatar({ src, alt, size = 40 }) {
		 return <img src={src} alt={alt} width={size} height={size} />;
	 }
	 // Usage: <Avatar src="/me.png" alt="Me" size={64} />
	 ```
	 </details>
   
12. What is state in React?
	 <details>
	 <summary>Answer</summary>
   
	 - Mutable data private to a component instance; changes trigger re-renders.
   
	 ```jsx
	 function Newsletter() {
		 const [email, setEmail] = React.useState("");
		 const [sent, setSent] = React.useState(false);
		 return sent ? (
			 <p>Thanks!</p>
		 ) : (
			 <form onSubmit={(e)=>{e.preventDefault(); setSent(true);}}>
				 <input value={email} onChange={(e)=>setEmail(e.target.value)} />
				 <button>Subscribe</button>
			 </form>
		 );
	 }
	 ```
	 </details>
   
13. Difference between props and state?
	 <details>
	 <summary>Answer</summary>
   
	 - Props: external, read-only, passed by parent; State: internal, mutable via setters.
	 - Props change when parents re-render; State changes via `setState`/`setX`.
   
	 ```mermaid
	 flowchart LR
		 Parent -- props --> Child
		 Child -- event (onClick) --> Parent
		 Child -- setState --> Child[Re-render]
	 ```
	 </details>
   
14. What is the Virtual DOM?
	 <details>
	 <summary>Answer</summary>
   
	 - An in-memory tree representation of the UI. React diffs the new tree vs previous and applies minimal DOM operations.
   
	 ```mermaid
	 sequenceDiagram
		 participant C as Component
		 participant V1 as Virtual DOM (prev)
		 participant V2 as Virtual DOM (next)
		 participant D as Real DOM
		 C->>V2: render()
		 V2->>V1: diff
		 V2->>D: patch changes
	 ```
	 </details>
   
15. How does React update the DOM?
	 <details>
	 <summary>Answer</summary>
   
	 - Render: compute next VDOM
	 - Reconcile: diff old vs new
	 - Commit: batch and apply DOM mutations; run layout effects
   
	 ```jsx
	 setCount(c => c + 1); // queues an update
	 // React batches updates and commits minimal DOM changes
	 ```
	 </details>
   
16. What is a single-page application (SPA)?
	 <details>
	 <summary>Answer</summary>
   
	 - An app that loads a single HTML page and updates the view dynamically via JavaScript without full page reloads.
   
	 Example: Navigating from `/products` to `/cart` updates the view instantly using client-side routing.
	 </details>
   
17. What is the difference between Real DOM and Virtual DOM?
	 <details>
	 <summary>Answer</summary>
   
	 - Real DOM: browser’s live UI tree; updates are comparatively slow.
	 - Virtual DOM: lightweight JS objects; diff first, then minimal real DOM updates.
   
	 Result: Better performance for many small updates.
	 </details>
   
18. What is React Fiber?
	 <details>
	 <summary>Answer</summary>
   
	 - The reconciliation engine introduced in React 16 enabling incremental rendering, prioritization, and interruption.
	 - Lets React pause, abort, or reuse work; improves responsiveness for large trees.
   
	 Example: While typing, low-priority UI updates can be deferred so input stays snappy.
	 </details>
   
19. What are fragments in React?
	 <details>
	 <summary>Answer</summary>
   
	 - A way to return multiple elements without adding extra DOM nodes.
   
	 ```jsx
	 function Row({ left, right }) {
		 return (<>
			 <td>{left}</td>
			 <td>{right}</td>
		 </>);
	 }
	 ```
	 </details>
   
20. How do you create a React app?
	 <details>
	 <summary>Answer</summary>
   
	 As of 2025, preferred starters are Vite (SPA), Next.js (SSR/SSG), or Remix. `create-react-app` is legacy for many cases.
   
	 Vite (SPA):
   
	 ```powershell
	 npm create vite@latest my-app -- --template react
	 cd my-app
	 npm install
	 npm run dev
	 ```
   
	 Next.js (SSR/SSG + routing):
   
	 ```powershell
	 npx create-next-app@latest my-app
	 cd my-app
	 npm run dev
	 ```
   
	 Notes:
	 - Choose Next.js if you need SEO, server components, or APIs.
	 - Choose Vite for fast SPAs with minimal config.
	 </details>

---

## 2. React Components & Lifecycle (21–40)

21. What are controlled components?
	 <details>
	 <summary>Answer</summary>
   
	 - Form inputs whose value is controlled by React state.
	 - The UI reflects state; updates happen via `onChange` that calls `setState`/`setX`.
   
	 ```jsx
	 function Login() {
		 const [email, setEmail] = React.useState("");
		 return (
			 <input value={email} onChange={(e)=>setEmail(e.target.value)} />
		 );
	 }
	 ```
   
	 Pros: Validation and formatting are centralized; easier to test.
	 </details>
   
22. What are uncontrolled components?
	 <details>
	 <summary>Answer</summary>
   
	 - Inputs that keep their own internal state in the DOM; React reads values via refs when needed.
   
	 ```jsx
	 function Login() {
		 const emailRef = React.useRef();
		 function handleSubmit(e){
			 e.preventDefault();
			 console.log(emailRef.current.value);
		 }
		 return (
			 <form onSubmit={handleSubmit}>
				 <input ref={emailRef} defaultValue="" />
				 <button>Submit</button>
			 </form>
		 );
	 }
	 ```
   
	 Pros: Less re-rendering; good for simple forms or large uncontrolled libraries.
	 </details>
   
23. What are React lifecycle methods?
	 <details>
	 <summary>Answer</summary>
   
	 - Class component hooks for mount, update, and unmount phases: `componentDidMount`, `componentDidUpdate`, `componentWillUnmount`, etc.
	 - In function components, use Hooks equivalents: `useEffect`, `useLayoutEffect`, `useInsertionEffect`.
   
	 ```mermaid
	 flowchart LR
		 Mount --> Update --> Unmount
	 ```
	 </details>
   
24. Explain `componentDidMount()`.
	 <details>
	 <summary>Answer</summary>
   
	 - Runs once after the component mounts; good for fetching data or subscribing to events.
	 - Hook equivalent: `useEffect(() => { ... }, [])`.
   
	 ```jsx
	 class Users extends React.Component {
		 state = { list: [] };
		 async componentDidMount(){
			 const res = await fetch('/api/users');
			 this.setState({ list: await res.json() });
		 }
		 render(){ return <ul>{this.state.list.map(u=> <li key={u.id}>{u.name}</li>)}</ul>; }
	 }
	 ```
	 </details>
   
25. Explain `componentDidUpdate()`.
	 <details>
	 <summary>Answer</summary>
   
	 - Invoked after updates; compare previous props/state to run side effects conditionally.
   
	 ```jsx
	 componentDidUpdate(prevProps){
		 if (prevProps.userId !== this.props.userId) {
			 this.loadUser();
		 }
	 }
	 ```
   
	 Hook equivalent: `useEffect(() => { loadUser(); }, [userId])`.
	 </details>
   
26. Explain `componentWillUnmount()`.
	 <details>
	 <summary>Answer</summary>
   
	 - Cleanup before the component is removed: cancel timers, remove listeners, abort fetches.
   
	 ```jsx
	 componentWillUnmount(){
		 clearInterval(this.timer);
		 window.removeEventListener('resize', this.onResize);
	 }
	 ```
   
	 Hook equivalent: `useEffect(() => { return () => cleanup(); }, [])`.
	 </details>
   
27. What is the use of `shouldComponentUpdate()`?
	 <details>
	 <summary>Answer</summary>
   
	 - Lets you skip re-renders by returning `false` when inputs haven’t changed.
	 - Prefer `PureComponent` or `React.memo` in modern code.
   
	 ```jsx
	 shouldComponentUpdate(nextProps){
		 return nextProps.value !== this.props.value;
	 }
	 ```
	 </details>
   
28. What is the difference between mounting and unmounting?
	 <details>
	 <summary>Answer</summary>
   
	 - Mounting: inserting the component into the DOM the first time.
	 - Unmounting: removing the component from the DOM.
   
	 ```mermaid
	 sequenceDiagram
		 participant A as App
		 participant D as DOM
		 A->>D: Mount <Modal />
		 A->>D: Unmount <Modal />
	 ```
	 </details>
   
29. What is pure component in React?
	 <details>
	 <summary>Answer</summary>
   
	 - `React.PureComponent` implements shallow prop/state comparison to avoid unnecessary re-renders.
	 - Functional equivalent: `React.memo(Component)`.
	 </details>
   
30. What are higher-order components (HOC)?
	 <details>
	 <summary>Answer</summary>
   
	 - A function that takes a component and returns a new component with enhanced behavior.
   
	 ```jsx
	 const withLoading = (Comp) => (props) => props.loading ? <Spinner/> : <Comp {...props}/>;
	 ```
   
	 Note: Hooks often replace HOCs for many patterns.
	 </details>
   
31. What are stateless components?
	 <details>
	 <summary>Answer</summary>
   
	 - Components that don’t manage state themselves; they just render based on props.
   
	 ```jsx
	 const Title = ({ text }) => <h1>{text}</h1>;
	 ```
	 </details>
   
32. What are stateful components?
	 <details>
	 <summary>Answer</summary>
   
	 - Components that hold their own state and manage it over time.
   
	 ```jsx
	 function Toggle(){
		 const [on, setOn] = React.useState(false);
		 return <button onClick={()=>setOn(o=>!o)}>{on ? 'ON' : 'OFF'}</button>;
	 }
	 ```
	 </details>
   
33. Difference between functional and class components?
	 <details>
	 <summary>Answer</summary>
   
	 - Functional: simpler, hooks-based, less boilerplate, easier testing.
	 - Class: lifecycle methods, `this`, can be verbose; legacy codebases.
   
	 Most new React uses functional components.
	 </details>
   
34. How to pass data from parent to child component?
	 <details>
	 <summary>Answer</summary>
   
	 - Via props.
   
	 ```jsx
	 function Parent(){
		 return <Child greeting="Hello" />;
	 }
	 function Child({ greeting }){ return <p>{greeting}</p>; }
	 ```
	 </details>
   
35. How to pass data from child to parent component?
	 <details>
	 <summary>Answer</summary>
   
	 - Pass a callback prop down; child calls it with data.
   
	 ```jsx
	 function Parent(){
		 const [value, setValue] = React.useState('');
		 return <Child onChange={setValue} />;
	 }
	 function Child({ onChange }){
		 return <input onChange={(e)=>onChange(e.target.value)} />;
	 }
	 ```
	 </details>
   
36. What are default props?
	 <details>
	 <summary>Answer</summary>
   
	 - Fallback values for props when not provided.
   
	 ```jsx
	 function Button({ variant = 'primary', children }){
		 return <button className={`btn btn-${variant}`}>{children}</button>;
	 }
	 ```
	 </details>
   
37. What are propTypes?
	 <details>
	 <summary>Answer</summary>
   
	 - Runtime type checking for props using the `prop-types` package.
   
	 ```jsx
	 import PropTypes from 'prop-types';
	 function Badge({ count }){ return <span>{count}</span>; }
	 Badge.propTypes = { count: PropTypes.number.isRequired };
	 ```
   
	 Note: TypeScript is preferred for static typing.
	 </details>
   
38. What is the key prop and why is it important?
	 <details>
	 <summary>Answer</summary>
   
	 - `key` helps React identify list items across renders to match elements and preserve state.
	 - Should be stable, unique, and predictable.
   
	 ```jsx
	 items.map(item => <li key={item.id}>{item.name}</li>)
	 ```
	 </details>
   
39. Why should keys be unique in lists?
	 <details>
	 <summary>Answer</summary>
   
	 - Duplicate keys break React’s diffing; items can swap state or re-render incorrectly.
   
	 ```mermaid
	 flowchart LR
		 Old[Old List] -->|keys| Diff
		 New[New List] -->|keys| Diff
		 Diff --> Patch
	 ```
	 </details>
   
40. What happens if you don’t pass a key in a list?
	 <details>
	 <summary>Answer</summary>
   
	 - React falls back to index as key, which can cause bugs when items are inserted/removed (state sticks to wrong item).
	 - Always use stable IDs when possible.
	 </details>

---

## 3. React Hooks (41–60)

41. What are React hooks?
	 <details>
	 <summary>Answer</summary>
   
	 - Hooks are functions that let you use state and other React features in function components.
	 - Core hooks include `useState`, `useEffect`, `useContext`, `useRef`, `useMemo`, `useCallback`, `useReducer`.
   
	 Real‑world: A chat input using `useState` for text and `useEffect` to auto-focus.
   
	 ```jsx
	 function ChatInput(){
		 const [msg, setMsg] = React.useState("");
		 const ref = React.useRef(null);
		 React.useEffect(()=>{ ref.current?.focus(); }, []);
		 return <input ref={ref} value={msg} onChange={(e)=>setMsg(e.target.value)} />;
	 }
	 ```
	 </details>
   
42. Why were hooks introduced?
	 <details>
	 <summary>Answer</summary>
   
	 - To reuse stateful logic without HOCs/render props; reduce complexity from classes; better code organization by concern.
	 - They simplify sharing logic (custom hooks) and avoid `this` pitfalls.
	 </details>
   
43. What is `useState()` hook?
	 <details>
	 <summary>Answer</summary>
   
	 - Returns a state value and a setter function; updates trigger re-renders.
   
	 ```jsx
	 const [count, setCount] = React.useState(0);
	 setCount(c => c + 1);
	 ```
	 </details>
   
44. What is `useEffect()` hook?
	 <details>
	 <summary>Answer</summary>
   
	 - Runs side effects after render. Dependencies array controls when it runs. Return a cleanup function if needed.
   
	 ```jsx
	 useEffect(() => {
		 const id = setInterval(tick, 1000);
		 return () => clearInterval(id);
	 }, []);
	 ```
	 </details>
   
45. Difference between `useEffect()` and lifecycle methods?
	 <details>
	 <summary>Answer</summary>
   
	 - `useEffect` combines `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` depending on deps.
	 - Effects run after paint; `useLayoutEffect` runs synchronously after DOM mutations (layout-sensitive work).
   
	 ```mermaid
	 flowchart LR
		 Render --> Effect[useEffect]
		 Effect --> Cleanup
	 ```
	 </details>
   
46. What is `useContext()` hook?
	 <details>
	 <summary>Answer</summary>
   
	 - Accesses a React context value from the nearest `<Context.Provider>`.
   
	 ```jsx
	 const Theme = React.createContext('light');
	 function Button(){
		 const theme = React.useContext(Theme);
		 return <button className={`btn-${theme}`}>OK</button>;
	 }
	 ```
	 </details>
   
47. What is `useReducer()` hook?
	 <details>
	 <summary>Answer</summary>
   
	 - Manages complex state transitions using a reducer function `(state, action) => newState`.
	 - Useful for multi-field forms, complex updates, or when you want predictable transitions.
   
	 ```jsx
	 function reducer(state, action){
		 switch(action.type){
			 case 'inc': return {...state, count: state.count+1};
			 case 'dec': return {...state, count: state.count-1};
			 default: return state;
		 }
	 }
	 const [state, dispatch] = React.useReducer(reducer, { count: 0 });
	 ```
	 </details>
   
48. What is `useMemo()` hook?
	 <details>
	 <summary>Answer</summary>
   
	 - Memoizes an expensive computation result until dependencies change.
   
	 ```jsx
	 const total = React.useMemo(() => items.reduce((s,i)=>s+i.price,0), [items]);
	 ```
	 </details>
   
49. What is `useCallback()` hook?
	 <details>
	 <summary>Answer</summary>
   
	 - Memoizes a function reference to avoid unnecessary re-renders in children expecting stable callbacks.
   
	 ```jsx
	 const onAdd = React.useCallback((p)=> cart.add(p), [cart]);
	 ```
	 </details>
   
50. What is `useRef()` hook?
	 <details>
	 <summary>Answer</summary>
   
	 - Holds a mutable value that doesn’t trigger re-renders; commonly used to reference DOM nodes.
   
	 ```jsx
	 const inputRef = React.useRef(null);
	 useEffect(()=> inputRef.current?.focus(), []);
	 ```
	 </details>
   
51. What is the difference between `useMemo` and `useCallback`?
	 <details>
	 <summary>Answer</summary>
   
	 - `useMemo(fn, deps)` returns a memoized value.
	 - `useCallback(fn, deps)` returns a memoized function (equivalent to `useMemo(() => fn, deps)`).
	 </details>
   
52. Can you use hooks inside loops or conditions? Why not?
	 <details>
	 <summary>Answer</summary>
   
	 - No. Hooks must run in the same order on every render so React can match state to hooks by index.
	 - Put hooks at the top level of the component or custom hook.
	 </details>
   
53. What are custom hooks?
	 <details>
	 <summary>Answer</summary>
   
	 - Reusable functions that call hooks to share stateful logic between components. Named with `use*`.
	 </details>
   
54. How do you create a custom hook?
	 <details>
	 <summary>Answer</summary>
   
	 Example: `useLocalStorage` to persist a value.
   
	 ```jsx
	 function useLocalStorage(key, initial){
		 const [value, setValue] = React.useState(()=>{
			 const raw = localStorage.getItem(key);
			 return raw ? JSON.parse(raw) : initial;
		 });
		 React.useEffect(()=>{
			 localStorage.setItem(key, JSON.stringify(value));
		 }, [key, value]);
		 return [value, setValue];
	 }
	 ```
	 </details>
   
55. What is the rules of hooks?
	 <details>
	 <summary>Answer</summary>
   
	 - Only call hooks at the top level (not inside loops/conditions).
	 - Only call hooks from React functions (components or custom hooks).
	 </details>
   
56. What happens if you break the rules of hooks?
	 <details>
	 <summary>Answer</summary>
   
	 - State gets associated with the wrong hook call; you’ll see errors like "Invalid hook call" or buggy behavior.
	 - Use ESLint `eslint-plugin-react-hooks` to catch violations.
	 </details>
   
57. Can you use multiple hooks in one component?
	 <details>
	 <summary>Answer</summary>
   
	 - Yes. Compose as many as needed; order must be consistent.
   
	 ```jsx
	 function Profile(){
		 const user = useUser();
		 const [tab, setTab] = useState('posts');
		 useEffect(()=>{ document.title = user.name; }, [user.name]);
		 // ...
	 }
	 ```
	 </details>
   
58. How do you fetch data with hooks?
	 <details>
	 <summary>Answer</summary>
   
	 - Use `useEffect` for lifecycle and cleanup; track `loading`/`error` state.
   
	 ```jsx
	 function Users(){
		 const [users, setUsers] = useState([]);
		 const [loading, setLoading] = useState(true);
		 const [error, setError] = useState(null);
		 useEffect(()=>{
			 let alive = true;
			 fetch('/api/users')
				 .then(r=> r.ok ? r.json() : Promise.reject(r))
				 .then(d=> { if(alive){ setUsers(d); setLoading(false); } })
				 .catch(e=> { if(alive){ setError(e); setLoading(false); } });
			 return () => { alive = false; };
		 }, []);
		 // render
	 }
	 ```
	 </details>
   
59. Difference between `useState` and `useReducer`?
	 <details>
	 <summary>Answer</summary>
   
	 - `useState`: simple state, local updates; quick to use.
	 - `useReducer`: complex state transitions, multiple related fields, or when you want to centralize logic.
	 </details>
   
60. Difference between controlled input with `useState` and uncontrolled input with `useRef`?
	 <details>
	 <summary>Answer</summary>
   
	 - Controlled (`useState`): React is source of truth, easy validation but more re-renders.
	 - Uncontrolled (`useRef`): DOM is source of truth, fewer renders, read value on submit.
   
	 ```mermaid
	 flowchart LR
		 Controlled -->|state| Input
		 Uncontrolled -->|ref read| Input
	 ```
	 </details>

---

## 4. React Router & Navigation (61–70)

61. What is React Router?
	<details>
	<summary>Answer</summary>
   
	- A routing library for React that maps URLs to components and manages navigation without full page reloads.
	- Real‑world: An e‑commerce app where `/products`, `/products/42`, and `/cart` render different screens without reloading.
   
	```mermaid
	flowchart LR
	  URL[/URL/] --> Router
	  Router -->|/| Home
	  Router -->|/products| Products
	  Router -->|/products/:id| ProductDetail
	  Router -->|/cart| Cart
	```
	</details>
   
62. Difference between `<BrowserRouter>` and `<HashRouter>`?
	<details>
	<summary>Answer</summary>
   
	- `<BrowserRouter>` uses the HTML5 history API with clean URLs like `/products/42` (requires server config to serve index.html for all routes).
	- `<HashRouter>` uses the hash `#/products/42`, which doesn’t require server rewrite rules (useful for static hosting without config).
   
	Real‑world: Deploying to GitHub Pages often uses `<HashRouter>` to avoid 404s on refresh.
	</details>
   
63. What is `<Route>` in React Router?
	<details>
	<summary>Answer</summary>
   
	- `<Route>` maps a path to a UI element in v6 via the `element` prop.
   
	```jsx
	<Routes>
	  <Route path="/about" element={<About/>} />
	</Routes>
	```
	</details>
   
64. What is `<Switch>` in React Router v5?
	<details>
	<summary>Answer</summary>
   
	- `<Switch>` renders the first child `<Route>` that matches in v5.
	- In v6, `<Routes>` replaces it with improved matching.
   
	```jsx
	// v5
	<Switch>
	  <Route path="/" exact component={Home} />
	  <Route path="/about" component={About} />
	</Switch>
	```
	</details>
   
65. What replaced `<Switch>` in React Router v6?
	<details>
	<summary>Answer</summary>
   
	- `<Routes>` with `element` prop and nested routes.
   
	```jsx
	// v6
	<Routes>
	  <Route path="/" element={<Home/>} />
	  <Route path="/about" element={<About/>} />
	</Routes>
	```
	</details>
   
66. How do you redirect in React Router?
	<details>
	<summary>Answer</summary>
   
	- In v6, use the `<Navigate to="/path" replace />` component or the `useNavigate()` hook.
   
	```jsx
	// Component-based redirect
	<Navigate to="/login" replace />
   
	// Programmatic
	const navigate = useNavigate();
	navigate('/cart');
	```
	</details>
   
67. How do you pass parameters in routes?
	<details>
	<summary>Answer</summary>
   
	- Define dynamic segments with `:id` and read them with `useParams()`.
   
	```jsx
	<Route path="/products/:id" element={<Product/>} />
	function Product(){
	  const { id } = useParams();
	  // fetch(`/api/products/${id}`)
	}
	```
	</details>
   
68. Difference between `useHistory`, `useNavigate`, and `useLocation`?
	<details>
	<summary>Answer</summary>
   
	- v5: `useHistory()` for navigation.
	- v6: `useNavigate()` replaces history navigation; `useLocation()` returns `{ pathname, search, state }`.
   
	```jsx
	const navigate = useNavigate();
	const location = useLocation();
	navigate('/checkout', { state: { from: location } });
	```
	</details>
   
69. How do you create nested routes?
	 <details>
	 <summary>Answer</summary>
   
	 - Use nested `<Route>` elements and `<Outlet/>` in the parent component.
   
	 ```jsx
	 <Route path="/settings" element={<Settings/>}>
		 <Route path="profile" element={<Profile/>} />
		 <Route path="billing" element={<Billing/>} />
	 </Route>
   
	 function Settings(){ return (<div><Tabs/><Outlet/></div>); }
	 ```
   
	 ```mermaid
	 flowchart TD
		 Settings --> Profile
		 Settings --> Billing
	 ```
	 </details>
   
70. How do you protect routes (authentication)?
	<details>
	<summary>Answer</summary>
   
	- Wrap protected routes with an auth gate that redirects unauthenticated users.
   
	```jsx
	function RequireAuth({ children }){
	  const user = useUser();
	  const location = useLocation();
	  if(!user) return <Navigate to="/login" state={{ from: location }} replace />;
	  return children;
	}
   
	<Route path="/dashboard" element={<RequireAuth><Dashboard/></RequireAuth>} />
	```
	</details>

---

## 5. State Management & Context (71–80)

71. What is prop drilling?
	<details>
	<summary>Answer</summary>
   
	- Passing data through multiple intermediate components that don’t need it, just to reach a deeply nested child.
   
	```mermaid
	flowchart LR
	  A[Parent] --> B[Mid]
	  B --> C[Deep Child]
	  A -- prop --> B
	  B -- prop --> C
	```
	</details>
   
72. How do you solve prop drilling?
	<details>
	<summary>Answer</summary>
   
	- Use Context for global-ish values, co-locate state, lift state carefully, or adopt a state manager (Redux, Zustand) when complex.
	- Component composition and render props can also help.
	</details>
   
73. What is Context API in React?
	<details>
	<summary>Answer</summary>
   
	- A mechanism to pass values down the tree without prop drilling using `createContext` and `<Provider>`.
   
	```jsx
	const Theme = React.createContext('light');
	function App(){
	  return <Theme.Provider value="dark"><Toolbar/></Theme.Provider>;
	}
	function Toolbar(){ return <Button/>; }
	function Button(){ const theme = React.useContext(Theme); return <button className={theme}>Buy</button>; }
	```
	</details>
   
74. How do you use Context API with hooks?
	<details>
	<summary>Answer</summary>
   
	- Use `useContext(MyContext)` inside function components to read the nearest provider’s value.
	- Combine with custom hooks for nicer APIs.
   
	```jsx
	const Auth = React.createContext(null);
	export function useAuth(){ return React.useContext(Auth); }
	```
	</details>
   
75. What are providers and consumers in Context?
	<details>
	<summary>Answer</summary>
   
	- Provider: component that supplies a value to its descendants.
	- Consumer: components that read the value (via `useContext` or `<Context.Consumer>` in legacy).
	</details>
   
76. What is Redux?
	<details>
	<summary>Answer</summary>
   
	- A predictable state container with a single store, actions, and pure reducers; excellent devtools.
	- Modern Redux is typically used via Redux Toolkit (RTK).
	</details>
   
77. What are the core principles of Redux?
	<details>
	<summary>Answer</summary>
   
	- Single source of truth
	- State is read-only (immutable updates)
	- Changes via pure reducers
	</details>
   
78. Difference between Redux and Context API?
	<details>
	<summary>Answer</summary>
   
	- Context is a transport mechanism for values; it doesn’t prescribe how to update state.
	- Redux provides a structured approach to state changes, middleware, tooling, time-travel, and good patterns for large apps.
	</details>
   
79. What are Redux middleware?
	<details>
	<summary>Answer</summary>
   
	- Functions that intercept dispatched actions for async, logging, or side effects (e.g., Thunk, Saga), configured in the store.
   
	```jsx
	import { configureStore } from '@reduxjs/toolkit';
	export const store = configureStore({ reducer, middleware: (gDM) => gDM().concat(myMiddleware) });
	```
	</details>
   
80. What is Redux Toolkit?
	<details>
	<summary>Answer</summary>
   
	- The official, batteries-included set of utilities for Redux that reduces boilerplate and encourages best practices.
   
	```jsx
	import { configureStore, createSlice } from '@reduxjs/toolkit';
	const cart = createSlice({
	  name: 'cart', initialState: { items: [] },
	  reducers: { add: (s,a)=>{ s.items.push(a.payload); } }
	});
	export const { add } = cart.actions;
	export const store = configureStore({ reducer: { cart: cart.reducer } });
	```
   
	```mermaid
	flowchart LR
	  UI -->|dispatch action| Reducer
	  Reducer --> Store
	  Store --> UI
	```
	</details>

---

## 6. Performance & Optimization (81–90)

81. How to optimize React performance?
	<details>
	<summary>Answer</summary>
   
	- Use `React.memo` for pure components; `useMemo`/`useCallback` for expensive values/handlers; list virtualization; code splitting; avoid unnecessary context re-renders; batch updates.
	- Measure with React DevTools Profiler.
	</details>
   
82. What is code splitting in React?
	<details>
	<summary>Answer</summary>
   
	- Splitting bundles into smaller chunks that are loaded on demand to reduce initial load time.
	- Achieved via dynamic `import()` and tooling (Vite/Webpack), often per route or component.
	</details>
   
83. What is lazy loading in React?
	<details>
	<summary>Answer</summary>
   
	- Defer loading of components until they’re needed using `React.lazy` and `Suspense`.
   
	```jsx
	const Settings = React.lazy(()=> import('./Settings'));
	<Suspense fallback={<Spinner/>}>
	  <Settings/>
	</Suspense>
	```
	</details>
   
84. What is React Suspense?
	<details>
	<summary>Answer</summary>
   
	- A mechanism to show a fallback while awaiting lazy components or data (with supported libraries). Works great with route-based splitting.
	</details>
   
85. What is memoization in React?
	<details>
	<summary>Answer</summary>
   
	- Caching results of computations to avoid recomputing on every render when inputs haven’t changed (`useMemo`), or caching component rendering (`React.memo`).
	</details>
   
86. Difference between `React.memo` and `useMemo`?
	<details>
	<summary>Answer</summary>
   
	- `React.memo(Component)`: memoizes a component’s rendered output based on props.
	- `useMemo(factory, deps)`: memoizes the result of a calculation used inside a component.
	</details>
   
87. What is reconciliation in React?
	<details>
	<summary>Answer</summary>
   
	- The process of diffing the new VDOM against the previous VDOM and applying minimal changes to the real DOM.
	</details>
   
88. What is diffing algorithm?
	<details>
	<summary>Answer</summary>
   
	- Heuristics React uses to compare trees efficiently: assumes different element types produce different trees; keys help preserve children.
	</details>
   
89. What is server-side rendering (SSR) in React?
	<details>
	<summary>Answer</summary>
   
	- Rendering React components on the server to HTML and sending it to the client for faster first paint and SEO.
	- Implemented by frameworks like Next.js.
   
	```mermaid
	sequenceDiagram
	  participant B as Browser
	  participant S as Server
	  B->>S: Request /
	  S-->>B: HTML (rendered markup)
	  B->>B: Hydrate with JS
	```
	</details>
   
90. What is hydration in React?
	<details>
	<summary>Answer</summary>
   
	- Attaching event listeners and making server-rendered HTML interactive on the client.
	- In React 18+, selective hydration and streaming improve time-to-interactive.
	</details>

---

## 7. Advanced Topics & Miscellaneous (91–100)

91. What is Next.js and how is it related to React?
	<details>
	<summary>Answer</summary>
   
	- A React framework providing file-based routing, SSR/SSG/ISR, API routes, image optimization, and React Server Components.
	- Great for SEO-heavy sites and apps needing hybrid rendering.
	</details>
   
92. What is Gatsby and how is it different from Next.js?
	<details>
	<summary>Answer</summary>
   
	- Gatsby focuses on static site generation with a GraphQL data layer; excellent for content sites that build ahead of time.
	- Next.js is more general-purpose with SSR/SSG/ISR and serverless APIs.
	</details>
   
93. What are React portals?
	<details>
	<summary>Answer</summary>
   
	- A way to render children into a DOM node outside the parent DOM hierarchy; useful for modals, tooltips.
   
	```jsx
	import { createPortal } from 'react-dom';
	function Modal({ children }){
	  return createPortal(children, document.getElementById('modal-root'));
	}
	```
	</details>
   
94. What are error boundaries in React?
	<details>
	<summary>Answer</summary>
   
	- Class components implementing `componentDidCatch`/`getDerivedStateFromError` to catch rendering errors in children and show fallback UI.
   
	```jsx
	class ErrorBoundary extends React.Component {
	  state = { hasError: false };
	  static getDerivedStateFromError(){ return { hasError: true }; }
	  componentDidCatch(error, info){ console.error(error, info); }
	  render(){ return this.state.hasError ? <Fallback/> : this.props.children; }
	}
	```
	</details>
   
95. What are synthetic events in React?
	<details>
	<summary>Answer</summary>
   
	- React’s cross-browser wrapper around browser events for consistent behavior and pooling (pooling is disabled in modern versions).
	</details>
   
96. Difference between controlled forms and uncontrolled forms?
	<details>
	<summary>Answer</summary>
   
	- Controlled: input value driven by React state; Uncontrolled: DOM manages state, read via refs. Choose based on validation complexity and performance.
	</details>
   
97. What is React.StrictMode?
	<details>
	<summary>Answer</summary>
   
	- A development-only wrapper that highlights potential problems by intentionally double-invoking certain lifecycle and effect setup to surface issues; no effect in production.
	</details>
   
98. What is concurrent rendering in React 18?
	<details>
	<summary>Answer</summary>
   
	- React can interrupt and prioritize rendering to keep apps responsive. Features include transitions and selective hydration.
   
	```jsx
	import { startTransition } from 'react';
	startTransition(() => setSearchQuery(q));
	```
	</details>
   
99. What are React 18’s notable features (automatic batching, `useId`)?
	<details>
	<summary>Answer</summary>
   
	- Automatic batching for state updates across async boundaries; `useId` for stable IDs across SSR/CSR; new streaming SSR APIs; `useDeferredValue` and `useTransition`.
	</details>
   
100. Difference between React, React Native, and React DOM?
	<details>
	<summary>Answer</summary>
   
	- React: core library (components, state, reconciliation).
	- React DOM: renderer for web browsers.
	- React Native: renderer for native mobile platforms (iOS/Android) using native widgets.
	</details>

---
