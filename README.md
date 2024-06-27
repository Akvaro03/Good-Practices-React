# Best Practices for React Developers

## Table of Contents
1. [Component Structure](#component-structure)
1. [Big Components](#big-components)
1. [Nesting Gotcha](#nesting-gotcha)
5. [Performance Optimization](#performance-optimization)
5. [Prop Drilling](#prop-drilling)
6. [Testing](#testing)

## Component Structure

- **Organize Files by Feature**: Group related components, styles, and tests within the same directory.

src/
  ├── features/
  │   ├── FeatureA/
  │   │   ├── FeatureAComponent.js
  │   │   ├── FeatureAComponent.css
  │   │   └── FeatureAComponent.test.js
  │   └── FeatureB/

## Big Components

- **Avoid Big Components**: Optimize your big component into other small components.

function App() {
    return (
        <main>
            <Navbar>
            <Article>
        </main>
    )
}

## Nesting Gotcha

- **Avoid re renders**: Every time the parent component render the children components re render.

//God
const Child = ({handleClick}) =>{
        return <Button onClick={handleClick}>button</Button>
}

function Parent(){
    const handleClick = () => console.log("click")
    return <Child handleClick={handleClick}>
}

//Avoid
function Parent(){
    const handleClick = () => console.log("click")
    const Child = () =>{
        return <Button onClick={handleClick}>button</Button>
    }
    return <Child>
}

## Performance Optimization

- **Memoization**: Use React.memo and useMemo to memoize components and values.

const MemoizedComponent = React.memo(MyComponent);

const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);

- **Lazy Loading**: Use React.lazy and Suspense to lazy load components.
const LazyComponent = React.lazy(() => import('./LazyComponent'));

const App = () => (
  <Suspense fallback={<div>Loading...</div>}>
    <LazyComponent />
  </Suspense>
);

## Prop Drilling

- **Avoid Prop Drilling**: Use React Context or Redux to provide or consume data at different levels.

## Prop Plowing

//Avoid
function Page() {
    const data = {
        id:23,
        name:"Alvaro"
    }
    return (
        </User id={data.id} name={data.name}>
    )
}

//God
function Page(){
    const data={
        id:23,
        name:"Alvaro"
    }
    return(
        </User {...data}>
    )
}

## Testing

- **Use Testing Libraries**: Use testing libraries like Jest and React Testing Library for writing unit and integration tests.

import { render, screen } from '@testing-library/react';
import MyComponent from './MyComponent';

test('renders component', () => {
  render(<MyComponent />);
  expect(screen.getByText('Hello, World!')).toBeInTheDocument();
});
