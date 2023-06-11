# Ex-05:
## DEVELOP A TO DO LIST USING REACT FRAMEWORK
### AIM:
The aim of this code is to create a simple To-Do List application using the React framework. The application allows users to add, edit, delete, and mark tasks as completed.
### ALGORITHM:
1. Import the necessary dependencies from the React library and the CSS file.
2. Create a functional component called "App" to represent the To-Do List application.
3. Initialize the state variables using the useState hook:
* "tasks" to store an array of tasks
* "newTask" to store the value of the input field for adding a new task
* "editTaskId" to store the ID of the task being edited (null if no task is being edited)
4. Implement functions to handle different actions:
* "handleAddTask": Creates a new task object and adds it to the tasks array.
* "handleEditTask": Updates the text of a task with the provided ID.
* "handleDeleteTask": Removes a task from the tasks array.
* "handleToggleComplete": Toggles the completed status of a task.
5. Render the UI elements using JSX:
* Display a heading for the application.
* Create an input field and a button for adding new tasks.
* Render a list of tasks using the map() function on the tasks array.
* Each task item is displayed as a list item with a checkbox, task text (editable or non-editable), and action buttons for editing and deleting.
* Conditionally render an input field or a span for the task text, based on whether the task is being edited or not.
* Apply appropriate CSS classes and styles to the UI elements to achieve the desired layout and functionality.
### PROGRAM:
#### App.js:
```javascript
import React, { useState } from 'react';
import './App.css';

function App() {
  const [tasks, setTasks] = useState([]);
  const [newTask, setNewTask] = useState('');
  const [editTaskId, setEditTaskId] = useState(null);

  const handleAddTask = () => {
    if (newTask.trim() !== '') {
      const newTaskItem = {
        id: Date.now(),
        text: newTask,
        completed: false,
      };
      setTasks([...tasks, newTaskItem]);
      setNewTask('');
    }
  };

  const handleEditTask = (id, newText) => {
    const updatedTasks = tasks.map((task) => {
      if (task.id === id) {
        return {
          ...task,
          text: newText,
        };
      }
      return task;
    });
    setTasks(updatedTasks);
    setEditTaskId(null);
  };

  const handleDeleteTask = (id) => {
    const updatedTasks = tasks.filter((task) => task.id !== id);
    setTasks(updatedTasks);
  };

  const handleToggleComplete = (id) => {
    const updatedTasks = tasks.map((task) => {
      if (task.id === id) {
        return {
          ...task,
          completed: !task.completed,
        };
      }
      return task;
    });
    setTasks(updatedTasks);
  };

  return (
    <div className="todo-app">
      <h1 style={{textAlign:"center"}}>TO-DO LIST</h1>
      <div className="task-input">
        <input
          type="text"
          value={newTask}
          onChange={(e) => setNewTask(e.target.value)}
          placeholder="Enter a new task"
        />
        <button onClick={handleAddTask}>Add</button>
      </div>
      <ul className="task-list">
        {tasks.map((task) => (
          <li key={task.id} className={task.completed ? 'completed' : ''}>
            <input
              type="checkbox"
              checked={task.completed}
              onChange={() => handleToggleComplete(task.id)}
            />
            {editTaskId === task.id ? (
              <input
                type="text"
                value={task.text}
                onChange={(e) => handleEditTask(task.id, e.target.value)}
              />
            ) : (
              <span>{task.text}</span>
            )}
            <div className="task-actions">
              {editTaskId === task.id ? (
                <button onClick={() => handleEditTask(task.id, task.text)}>Save</button>
              ) : (
                <button onClick={() => setEditTaskId(task.id)}>Edit</button>
              )}
              <button onClick={() => handleDeleteTask(task.id)}>Delete</button>
            </div>
          </li>
        ))}
      </ul>
    </div>
  );
}
export default App;
```
#### App.css:
```css
.todo-app {
  width: 400px;
  margin: 50px auto;
  background-color:rgb(83, 202, 209);
  padding:20px;
}

.task-input {
  display: flex;
  margin-bottom: 10px;
}

.task-input input[type='text'] {
  flex-grow: 1;
  height: 30px;
  font-size: 16px;
  padding: 5px;
}

.task-input button {
  height: 30px;
  margin-left: 10px;
  background-color: #0b5b54;
  color: #fff;
  border: none;
  cursor: pointer;
}

.task-list {
  list-style: none;
  padding: 0;
}

.task-list li {
  display: flex;
  align-items: center;
  padding: 10px;
  background-color: #f1f1f1;
  margin-bottom: 5px;
  text-decoration: none;
}

.task-list li.completed span {
  text-decoration: line-through;
}

.task-list li input[type='checkbox'] {
  margin-right: 10px;
}

.task-list li input[type='text'] {
  flex-grow: 1;
  height: 25px;
  font-size: 14px;
  padding: 3px;
}

.task-list li button {
  margin-left: 10px;
  background-color: #ff4d4dba;
  color: #fff;
  border: none;
  cursor: pointer;
}
.task-actions {
  display: flex;
}

.task-actions button {
  margin-left: 5px;
}
```
### OUTPUT:

<img width="340" alt="image" src="https://github.com/KeerthikaNagarajan/React-Todolist/assets/93427089/1cc733d8-0f12-4221-8926-d9d2c4a7c1b3">

<img width="342" alt="image" src="https://github.com/KeerthikaNagarajan/React-Todolist/assets/93427089/9fa0435c-36d0-4a2f-837d-bb50004f7e25">

### RESULT:
The code will generate a To-Do List application with a simple user interface. 
