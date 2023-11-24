<template>
    <section class="">
        <div class="justify-center mt-5">
            <div class="text-center flex w-[400px] h-[30px] bg-gray-700 border border-blue-600 mx-auto ">
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-8 h-8 p-2 text-white">
                 <path stroke-linecap="round" stroke-linejoin="round" d="M21 21l-5.197-5.197m0 0A7.5 7.5 0 105.196 5.196a7.5 7.5 0 0010.607 10.607z" />
                </svg>
                <input type="text" v-model="todo" class="bg-transparent mx-auto focus:none  focus:outline-none" placeholder=" Create todo type...">
            </div>
            <div v-for="todo in todoList" :key="todo.text" class="justify-between flex w-[400px] h-[30px] bg-white border border-blue-600 mx-auto mt-5">
                <ul class="list-disc ml-3">
                    <li v-if="todo.completed" class="ml-3 text-green-500">{{ todo.text }}</li>
                    <li v-else class="ml-3 text-gray-500">{{ todo.text }}</li>
                </ul>
                <div class="flex">
                <button v-if="!todo.completed"  @click="completeLi(todo)" class="pr-3"><svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
  <path stroke-linecap="round" stroke-linejoin="round" d="M15 11.25l1.5 1.5.75-.75V8.758l2.276-.61a3 3 0 10-3.675-3.675l-.61 2.277H12l-.75.75 1.5 1.5M15 11.25l-8.47 8.47c-.34.34-.8.53-1.28.53s-.94.19-1.28.53l-.97.97-.75-.75.97-.97c.34-.34.53-.8.53-1.28s.19-.94.53-1.28L12.75 9M15 11.25L12.75 9" />
</svg>
</button>
                <button @click="deleteTodo(todo)" class="mr-3"><svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6 text-red-600">
  <path stroke-linecap="round" stroke-linejoin="round" d="M20.25 7.5l-.625 10.632a2.25 2.25 0 01-2.247 2.118H6.622a2.25 2.25 0 01-2.247-2.118L3.75 7.5M10 11.25h4M3.375 7.5h17.25c.621 0 1.125-.504 1.125-1.125v-1.5c0-.621-.504-1.125-1.125-1.125H3.375c-.621 0-1.125.504-1.125 1.125v1.5c0 .621.504 1.125 1.125 1.125z" />
</svg>
</button>
</div>
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
    data(){
        return{
            todo:'',
            todoList:[]
        }
    },
    methods:{
        addTodo(){
            let id = new Date().getTime()
            this.todoList.push(
                {text:this.todo, completed:false, id: id}
            )
            this.todo=''
            console.log(this.todoList);
        },
        deleteTodo(todo){
            const index=this.todoList.indexOf(todo)
            this.todoList.splice(index,1)
        },
        completeLi(todo){
            const index=this.todoList.indexOf(todo)
            this.todoList.splice(index,1)
            this.todoList.push(
                {text:todo.text, completed:true, id: todo.id}
            )
            this.todoList.sort((a,b)=>a.id-b.id)
        }
        
    }
}
</script>