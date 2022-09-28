<template>
    <div class="container">
        <div class="buttons">
            <button @click="deleteDoneTodos" class="button">Remove <span>Done</span> Tasks</button>
            <button @click="deleteAllTodos" class="button">Remove All Tasks</button>
        </div>
    </div>
</template>

<script>
import router from '../router';
    export default {
        setup() {

            const deleteDoneTodos = () => {
                let confirm = prompt("You are trying delete all \"done\" to-dos from your list. To continue, please type \"delete\" in this area.")
                
                if(confirm != null && confirm === "delete") {
                    let todos = JSON.parse(localStorage.getItem('todos'));
                    const res = todos.filter((obj) => obj.done !== true)
                    localStorage.setItem('todos', JSON.stringify(res))
                    router.push('/');
                }
            }

            const deleteAllTodos = () => {
                let confirm = prompt("You are trying delete ALL to-dos from your list. To continue, please type \"delete\" in this area.")

                if (confirm != null && confirm === "delete") {
                    localStorage.removeItem('todos');
                    router.push('/');
                }
            }
            
            return {
                deleteDoneTodos,
                deleteAllTodos,
            }
        }
    }
</script>

<style lang="scss">
.container {
    margin: .5rem;
}

.buttons {
    display: flex;
    justify-content: space-around;
}

.button {
    background-color: #be2d2f;
    color: antiquewhite;
    margin-inline: .5rem;
    font: {
        family: 'Poppins', sans-serif;
        weight: 500;
    }
    border-radius: .5rem;
    padding: .25rem;
    filter: drop-shadow(2px 2px rgb(107, 107, 107));
    transition: filter, transform 0.15s ease-in-out;
    cursor: pointer;

    &, &:focus, &:focus-within, &:active, &:hover {
        border: none;
        outline: none;
    }

    &:hover {
        filter: drop-shadow(0 0);
        transform: translate(2px, 2px);
    }

    &>span {
        color: #4bf04b;
    }
}
</style>