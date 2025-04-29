# React-Hands-on-Interview-Question

## Create a simple counter component with increment and decrement buttons.

### Solution -

```
import { useState } from "react";
import "./styles.css";

export default function App() {
  const [counter, setCounter] = useState(0);

  const handleIncrement = () => {
    setCounter(prev => prev + 1);
  };

  const handleDecrement = () => {
    setCounter(prev => Math.max(prev - 1, 0));
  };

  return (
    <div className="App">
      <h1>Count: {counter}</h1>
      <div>
        <button onClick={handleIncrement}>Increase</button>
        <button onClick={handleDecrement} disabled={counter === 0}>
          Decrease
        </button>
      </div>
    </div>
  );
}

```


## Create a Todo List app with Add, Delete, and Mark Completed features.

### Solution -

```

```

## Create a Modal component using React Portal.

### Solution -

```

```

## Build a custom hook useDebounce that delays updating a value.

### Solution -

```

```

## Build a simple Tabs component (Switch between tab contents).

### Solution -

```

```

## Implement a Search component that fetches and filters list items as you type.

### Solution -

```

```

## Create a Dropdown component using only React hooks.

### Solution -

```

```

## Implement a Dark Mode toggle using Context API.

### Solution -

```

```

## Build a reusable Accordion component.

### Solution -

```

```

## Create a Form with multiple inputs and validate them (name, email, password) in React.

### Solution -

```

```
