# React-Hands-on-Interview-Question

## 1. Create a simple counter component with increment and decrement buttons.

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


## 2. Create a Todo List app with Add, Delete, and Mark Completed features.

### Solution -

```

```

## 3. Create a Modal component using React Portal.

### Solution -

```

```

## 4. Build a custom hook useDebounce that delays updating a value.

### Solution -

```

```

## 5. Build a simple Tabs component (Switch between tab contents).

### Solution -

```

```

## 6. Implement a Search component that fetches and filters list items as you type.

### Solution -

```

```

## 7. Create a Dropdown component using only React hooks.

### Solution -

```

```

## 8. Implement a Dark Mode toggle using Context API.

### Solution -

```

```

## 9. Build a reusable Accordion component.

### Solution -

```

```

## 10. Create a Form with multiple inputs and validate them (name, email, password) in React.

### Solution -

```

```
