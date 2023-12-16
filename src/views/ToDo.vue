<template>
    <!-- Todo App -->
    <div class="main">
        <div class="container border-dark py-10">
            <div class="title">
                <h1 class="text-cyan-700 text-5xl mb-14">Todo App</h1>
            </div>
            <div class="actions">
                <form @submit.prevent="addTask">
                    <div class="search">
                        <input type="text" placeholder="Search task" v-model="searchQuery" />
                     </div>

                    <input type="text" placeholder="Add Task" v-model="task" required />
                    <button class="ml-2" type="submit">Add</button>
                    
                </form>
            </div>
            <div class="tasks">
                <div class="task-items" v-for="todo in filteredTodos" :key="todo.id">
                    <p :class="{ 'line-through': todo.done }" class="mx-4">{{ todo.details }}</p>
                    <button class="done-btn mx-2" @click="markAsDone(todo.id)">Done</button>
                    <button class="remove-btn" @click="removeTask(todo.id)">Remove</button>
                </div>
                <button class="clear-btn" @click="clearAllTasks">Clear ALL tasks</button>
            </div>
        </div>
    </div>
</template>

<script setup>
import database from '../firebase';
import { ref, computed, onMounted } from 'vue';
import { collection, addDoc, getDocs, deleteDoc, updateDoc, doc } from 'firebase/firestore';

const db = database;
const task = ref('');
const searchQuery = ref('');
const todos = ref([]);

// Function to fetch tasks from Firestore
const fetchTasks = async () => {
try {
    const querySnapshot = await getDocs(collection(db, 'tasks'));
    todos.value = querySnapshot.docs.map(doc => ({ ...doc.data(), id: doc.id }));
} catch (error) {
    console.error('Error fetching tasks:', error);
}
};

// Fetch tasks on component mount
onMounted(fetchTasks);

const addTask = async () => {
try {
    if (task.value.trim() !== '') {
        const newTask = { details: task.value, done: false };
        const docRef = await addDoc(collection(db, 'tasks'), newTask);
        todos.value.push({ ...newTask, id: docRef.id });
        task.value = '';
    }
} catch (error) {
    console.error('Error adding task:', error);
}
};

const removeTask = async (taskId) => {
try {
    await deleteDoc(doc(db, 'tasks', taskId));
    todos.value = todos.value.filter((todo) => todo.id !== taskId);
} catch (error) {
    console.error('Error removing task:', error);
}
};

const markAsDone = async (taskId) => {
try {
    const todo = todos.value.find((t) => t.id === taskId);
    if (todo) {
        await updateDoc(doc(db, 'tasks', taskId), { done: !todo.done });
        todo.done = !todo.done;
    }
} catch (error) {
    console.error('Error updating task:', error);
}
};

const clearAllTasks = async () => {
try {
    const querySnapshot = await getDocs(collection(db, 'tasks'));
    querySnapshot.forEach(async (doc) => {
        await deleteDoc(doc.ref);
    });
    todos.value = [];
} catch (error) {
    console.error('Error clearing all tasks:', error);
}
};

const filteredTodos = computed(() => {
return todos.value.filter((todo) =>
    todo.details.toLowerCase().includes(searchQuery.value.toLowerCase())
);
});
</script>

<style scoped>
.main {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
    background-color: rgb(203, 229, 255);
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
}

.container {
    text-align: center;
    background: #ffffff;
    border: solid black;
    width: 400px;
    border-radius: 10px;
/* Center align the content within the container */
}

.title {
    margin-bottom: 20px;
/* Add some space below the title */
}

.actions {
    margin-bottom: 20px;
/* Add some space below the actions */
}

input[type="text"] {
    width: 250px;
    padding: 8px;
    margin-right: 8px;
    border: 1px solid #ccc;
    border-radius: 4px;
}

button {
    padding: 8px 16px;
    background-color: #e6ffed; /* Light blue for "Done" button */
    color: #00e60f; /* Dark blue text color */
    border: 1px solid #b3ffbd; /* Border color */
    border-radius: 5px;
    cursor: pointer;
}

button.done-btn {
    background-color: #e6f7ff; /* Light blue for "Done" button */
    color: #0073e6; /* Dark blue text color */
    border: 1px solid #b3daff; /* Border color */
}

button.remove-btn {
    background-color: #ffe6e6; /* Light red for "Remove" button */
    color: #ff3333; /* Dark red text color */
    border: 1px solid #ffb3b3; /* Border color */
}

button.clear-btn {
    background-color: #ffe6e6; /* Light red for "Remove" button */
    color: #ff3333; /* Dark red text color */
    border: 1px solid #ffb3b3; /* Border color */
}

.tasks {
text-align: center;
/* Center align the content within the tasks div */
}

.task-items {
display: flex;
align-items: center;
justify-content: center;
margin-bottom: 10px;
/* Add some space between task items */
}

.line-through {
text-decoration: line-through;
}

.search{
    margin-bottom: 20px;

}
</style>


