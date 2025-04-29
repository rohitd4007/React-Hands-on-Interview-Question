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
import { useState } from "react";
import "./styles.css";

export default function App() {
  const [list, setList] = useState([]);
  const [userTask, setUserTask] = useState("");

  const addToDo = (task) => {
    if (!task.trim()) return;
    const newTask = {
      id: Date.now(),
      text: task,
      completed: false
    };
    setList((prev) => [...prev, newTask]);
    setUserTask("");
  };

  const deleteToDo = (id) => {
    const updatedList = list.filter((item, i) => item.id == id);
    setList(updatedList);
  };

  const toggleComplete = (id) => {
    const updatedList = list.map((item) =>
      item.id === id ? { ...item, completed: !item.completed } : item
    );
    setList(updatedList);
  };

  return (
    <div className="App">
      <h2>Add New Task</h2>
      <input
        value={userTask}
        onChange={(e) => setUserTask(e.target.value)}
        placeholder="Enter your task"
      />
      <button onClick={() => addToDo(userTask)}>Submit</button>

      <ul>
        {list.map((item) => (
          <li
            key={item.id}
            style={{
              marginTop: "10px",
              textDecoration: item.completed ? "line-through" : "none"
            }}
          >
            {item.text}
            <input
              type="checkbox"
              checked={item.completed}
              onChange={() => toggleComplete(item.id)}
              style={{ marginLeft: "10px" }}
            />
            <button
              onClick={() => deleteToDo(item.id)}
              style={{ marginLeft: "10px" }}
            >
              Delete
            </button>
          </li>
        ))}
      </ul>
    </div>
  );
}

```

## 3. Create a Modal component using React Portal.

### Solution -

#### index.html
```
<body>
  <div id="root"></div>
  <div id="modal-root"></div>
</body>

```

#### modal.js
```
// Modal.js
import React from "react";
import ReactDOM from "react-dom";

const Modal = ({ isOpen, onClose, children }) => {
  if (!isOpen) return null;

  return ReactDOM.createPortal(
    <div style={modalStyles.overlay}>
      <div style={modalStyles.modal}>
        <button style={modalStyles.closeBtn} onClick={onClose}>❌</button>
        {children}
      </div>
    </div>,
    document.getElementById("modal-root")
  );
};

const modalStyles = {
  overlay: {
    position: "fixed",
    top: 0, left: 0,
    width: "100vw", height: "100vh",
    backgroundColor: "rgba(0, 0, 0, 0.5)",
    display: "flex", justifyContent: "center", alignItems: "center"
  },
  modal: {
    background: "#fff",
    padding: "20px",
    borderRadius: "8px",
    minWidth: "300px",
    boxShadow: "0 2px 10px rgba(0, 0, 0, 0.3)"
  },
  closeBtn: {
    position: "absolute",
    top: 10,
    right: 10,
    background: "none",
    border: "none",
    fontSize: "20px",
    cursor: "pointer"
  }
};

export default Modal;

```
#### app.js

````
// App.js
import React, { useState } from "react";
import Modal from "./Modal";

export default function App() {
  const [isOpen, setIsOpen] = useState(false);

  return (
    <div className="App">
      <h1>React Modal Example</h1>
      <button onClick={() => setIsOpen(true)}>Open Modal</button>

      <Modal isOpen={isOpen} onClose={() => setIsOpen(false)}>
        <h2>Hello from Modal!</h2>
        <p>This modal is rendered using a portal!</p>
      </Modal>
    </div>
  );
}


````


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
