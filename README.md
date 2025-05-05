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
const useDebounce = (value, delay = 500) => {
  const [debouncedValue, setDebouncedValue] = useState(value);

  useEffect(() => {
    const handler = setTimeout(() => {
      setDebouncedValue(value);
    }, delay);

    return () => {
      clearTimeout(handler);
    };
  }, [value, delay]);

  return debouncedValue;
};

```

## 5. Build a simple Tabs component (Switch between tab contents).

### Solution -

```
import { useState } from "react";
import "./styles.css";

export default function App() {
  const [tab, setTab] = useState(0);

  const handlTabChange = (id) => {
    setTab(id);
  };

  const tabContent = [
    "This is content of Tab 1",
    "Here is Tab 2 content",
    "Welcome to Tab 3",
    "Final content from Tab 4"
  ];

  return (
    <div className="App">
      <div style={{ display: "flex", gap: "10px", marginBottom: "1rem" }}>
        <button onClick={() => handlTabChange(0)}>Tab 1</button>
        <button onClick={() => handlTabChange(1)}>Tab 2</button>
        <button onClick={() => handlTabChange(2)}>Tab 3</button>
        <button onClick={() => handlTabChange(3)}>Tab 4</button>
      </div>
      <div style={{ padding: "1rem", border: "1px solid #ccc" }}>
        {tabContent[tab]}
      </div>
    </div>
  );
}

```

## 6. Implement a Search component that fetches and filters list items as you type.

### Solution -

```
import { useState, useEffect } from "react";

export default function App() {
  const listItems = [
    { name: "Mango", id: 1 },
    { name: "Banana", id: 2 },
    { name: "Peru", id: 3 },
    { name: "Keshar", id: 4 },
    { name: "Pineapple", id: 5 },
  ];

  const [text, setText] = useState("");
  const [displayText, setDisplayText] = useState([]);

  useEffect(() => {
    const filteredList = listItems.filter((item) =>
      item.name.toLowerCase().startsWith(text.toLowerCase())
    );
    setDisplayText(filteredList);
  }, [text]);

  return (
    <div className="App">
      <input
        placeholder="Search fruits..."
        value={text}
        onChange={(e) => setText(e.target.value)}
        style={{ padding: "8px", width: "200px" }}
      />
      {displayText.length > 0 ? (
        displayText.map((item) => <div key={item.id}>{item.name}</div>)
      ) : (
        <div>No results found</div>
      )}
    </div>
  );
}

```

## 7. Create a Dropdown component using only React hooks.

### Solution -

```
// Dropdown.js
import { useState, useRef, useEffect } from "react";

const Dropdown = ({ options, selected, onSelect }) => {
  const [open, setOpen] = useState(false);
  const dropdownRef = useRef(null);

  const handleOutsideClick = (e) => {
    if (dropdownRef.current && !dropdownRef.current.contains(e.target)) {
      setOpen(false);
    }
  };

  useEffect(() => {
    document.addEventListener("mousedown", handleOutsideClick);
    return () => document.removeEventListener("mousedown", handleOutsideClick);
  }, []);

  return (
    <div ref={dropdownRef} style={{ position: "relative", width: "200px" }}>
      <div
        onClick={() => setOpen((prev) => !prev)}
        style={{ border: "1px solid black", padding: "10px", cursor: "pointer" }}
      >
        {selected || "Select an option"}
      </div>
      {open && (
        <ul
          style={{
            position: "absolute",
            border: "1px solid black",
            width: "100%",
            listStyle: "none",
            padding: 0,
            margin: 0,
            background: "white",
            zIndex: 10,
          }}
        >
          {options.map((option, i) => (
            <li
              key={i}
              style={{ padding: "10px", cursor: "pointer" }}
              onClick={() => {
                onSelect(option);
                setOpen(false);
              }}
            >
              {option}
            </li>
          ))}
        </ul>
      )}
    </div>
  );
};

export default Dropdown;

```
How to use it?

```
// App.js
import { useState } from "react";
import Dropdown from "./Dropdown";

export default function App() {
  const [selected, setSelected] = useState(null);

  return (
    <div className="App">
      <h2>Dropdown</h2>
      <Dropdown
        options={["Mango", "Apple", "Banana"]}
        selected={selected}
        onSelect={setSelected}
      />
      <p>Selected: {selected}</p>
    </div>
  );
}

```
## 8. Implement a Dark Mode toggle using Context API.

### Solution -
* Folder Structure
```
src/
├── App.js
├── styles.css
├── toggleContext.js
├── ToggleProvider.js
├── index.js

```
* 1. Create Context
```
// toggleContext.js
import { createContext } from "react";

// This will provide { darkMode, toggleDarkMode }
const ToggleContext = createContext();

export default ToggleContext;

```
* 2. Create Provider Component
```
// ToggleProvider.js
import { useState } from "react";
import ToggleContext from "./toggleContext";

const ToggleProvider = ({ children }) => {
  const [darkMode, setDarkMode] = useState(false);

  const toggleDarkMode = () => setDarkMode((prev) => !prev);

  return (
    <ToggleContext.Provider value={{ darkMode, toggleDarkMode }}>
      {children}
    </ToggleContext.Provider>
  );
};

export default ToggleProvider;

```
* 3. use Provider in index.js

```
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import App from "./App";
import ToggleProvider from "./ToggleProvider";

const root = createRoot(document.getElementById("root"));

root.render(
  <StrictMode>
    <ToggleProvider>
      <App />
    </ToggleProvider>
  </StrictMode>
);

```

* 4. Use Context in App

```
// App.js
import { useContext } from "react";
import ToggleContext from "./toggleContext";
import "./styles.css";

export default function App() {
  const { darkMode, toggleDarkMode } = useContext(ToggleContext);

  return (
    <div className={`App ${darkMode ? "isDark" : ""}`}>
      <label>
        <input type="checkbox" checked={darkMode} onChange={toggleDarkMode} />
        Dark Mode
      </label>
      <h1>This is App component</h1>
    </div>
  );
}

```

## 9. Build a reusable Accordion component.

### Solution -

```
// Accordion.js
import { useState } from "react";

const Accordion = ({ items }) => {
  const [activeIndex, setActiveIndex] = useState(null);

  const handleClick = (index) => {
    setActiveIndex((prev) => (prev === index ? null : index));
  };

  return (
    <div style={{ width: "400px", margin: "auto" }}>
      {items.map((item, i) => (
        <div key={i}>
          <div
            onClick={() => handleClick(i)}
            style={{
              padding: "10px",
              background: "#f0f0f0",
              cursor: "pointer",
              borderBottom: "1px solid gray",
            }}
          >
            {item.title}
          </div>
          {activeIndex === i && (
            <div style={{ padding: "10px", background: "#fff" }}>{item.content}</div>
          )}
        </div>
      ))}
    </div>
  );
};

export default Accordion;

```
How to use Accordian Component?
```
// App.js
import Accordion from "./Accordion";

const items = [
  { title: "What is React?", content: "A JavaScript library for building UI." },
  { title: "Why use React?", content: "It’s flexible, fast, and declarative." },
  { title: "How to use React?", content: "By creating components!" },
];

export default function App() {
  return (
    <div className="App">
      <h2>Accordion</h2>
      <Accordion items={items} />
    </div>
  );
}

```

## 10. Create a Form with multiple inputs and validate them (name, email, password) in React.

### Solution -

```
import { useState } from "react";

export default function App() {
  const [formData, setFormData] = useState({ name: "", email: "", password: "" });
  const [errors, setErrors] = useState({});

  const validate = () => {
    const errs = {};

    if (!formData.name.trim()) errs.name = "Name is required.";
    if (!formData.email.includes("@")) errs.email = "Invalid email.";
    if (formData.password.length < 6) errs.password = "Password too short.";

    setErrors(errs);
    return Object.keys(errs).length === 0;
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    if (validate()) {
      alert("Form submitted successfully!");
      setFormData({ name: "", email: "", password: "" });
    }
  };

  const handleChange = (e) => {
    const { name, value } = e.target;
    setFormData((prev) => ({ ...prev, [name]: value }));
  };

  return (
    <div className="App">
      <h2>Validated Form</h2>
      <form onSubmit={handleSubmit}>
        <div>
          Name: <input name="name" value={formData.name} onChange={handleChange} />
          <div style={{ color: "red" }}>{errors.name}</div>
        </div>
        <div>
          Email: <input name="email" value={formData.email} onChange={handleChange} />
          <div style={{ color: "red" }}>{errors.email}</div>
        </div>
        <div>
          Password:{" "}
          <input
            name="password"
            type="password"
            value={formData.password}
            onChange={handleChange}
          />
          <div style={{ color: "red" }}>{errors.password}</div>
        </div>
        <button type="submit">Submit</button>
      </form>
    </div>
  );
}

```
