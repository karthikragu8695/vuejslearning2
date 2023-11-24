<template>
    <section class="hidden">
        <div class="justify-center mt-5">
            <div class="text-center flex w-[400px] h-[30px] bg-gray-700 border border-blue-600 mx-auto ">
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-8 h-8 p-2 text-white">
                 <path stroke-linecap="round" stroke-linejoin="round" d="M21 21l-5.197-5.197m0 0A7.5 7.5 0 105.196 5.196a7.5 7.5 0 0010.607 10.607z" />
                </svg>
                <input type="text" v-model="todo" class="bg-transparent mx-auto focus:none  focus:outline-none" placeholder=" Create todo type...">
            </div>
            <div v-for="todo in todoList" :key="todo.id" class="justify-between flex w-[400px] h-[30px] bg-white border border-blue-600 mx-auto mt-5">
                <ul class="list-disc ml-3">
                    <li class="ml-3">{{ todo }}</li>
                </ul>
                <button @click="deleteTodo(todo)" class="mr-3"><svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6 text-red-600">
  <path stroke-linecap="round" stroke-linejoin="round" d="M20.25 7.5l-.625 10.632a2.25 2.25 0 01-2.247 2.118H6.622a2.25 2.25 0 01-2.247-2.118L3.75 7.5M10 11.25h4M3.375 7.5h17.25c.621 0 1.125-.504 1.125-1.125v-1.5c0-.621-.504-1.125-1.125-1.125H3.375c-.621 0-1.125.504-1.125 1.125v1.5c0 .621.504 1.125 1.125 1.125z" />
</svg>
</button>
            </div>
            <div class=" w-[400px] h-[30px]  bg-gray-700 border border-black hover:border-blue-500 text-center mx-auto mt-5">
                <button @click="addTodo()" class="text-white ">Add New todo...</button>

            </div>
        </div>
    </section>
</template>

<!----------------script--------------------->
<script>
export default{
    name:'emp-form',
    data(){
        return{
            todo:'',
            todoList:[]
        }
    },
    methods:{
        addTodo(){
            this.todoList.push(this.todo)
            this.todo=''
        },
        deleteTodo(todo){
            const index=this.todoList.indexOf(todo)
            this.todoList.splice(index,1)
        },
    }
}
</script>