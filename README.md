# meridianimport { useState } from "react";

export default function TodoList() {
  const [tasks, setTasks] = useState([]);
  const [task, setTask] = useState("");

  const addTask = () => {
    if (task.trim()) {
      setTasks([...tasks, { id: Date.now(), text: task, done: false }]);
      setTask("");
    }
  };

  const toggleTask = (id) => {
    setTasks(tasks.map(t => t.id === id ? { ...t, done: !t.done } : t));
  };

  const deleteTask = (id) => {
    setTasks(tasks.filter(t => t.id !== id));
  };

  return (
    <div style={{ maxWidth: "400px", margin: "auto", padding: "20px" }}>
      <h1 style={{ fontSize: "1.5rem", fontWeight: "bold", marginBottom: "10px" }}>To-Do List</h1>
      <div style={{ display: "flex", gap: "10px", marginBottom: "10px" }}>
        <input 
          value={task} 
          onChange={(e) => setTask(e.target.value)} 
          placeholder="Add a new task" 
          style={{ flex: 1, padding: "8px" }}
        />
        <button onClick={addTask} style={{ padding: "8px 12px", cursor: "pointer" }}>Add</button>
      </div>
      <ul style={{ listStyle: "none", padding: 0 }}>
        {tasks.map(t => (
          <li 
            key={t.id} 
            style={{ 
              display: "flex", 
              justifyContent: "space-between", 
              padding: "8px", 
              border: "1px solid #ddd", 
              marginBottom: "5px" 
            }}
          >
            <span 
              onClick={() => toggleTask(t.id)}
              style={{ 
                textDecoration: t.done ? "line-through" : "none", 
                cursor: "pointer" 
              }}
            >
              {t.text}
            </span>
            <button onClick={() => deleteTask(t.id)} style={{ cursor: "pointer" }}>❌</button>
          </li>
        ))}
      </ul>
    </div>
  );
}
