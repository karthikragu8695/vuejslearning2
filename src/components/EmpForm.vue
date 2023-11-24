<template>
    <section class="flex justify-center">
        <div class="justify-center mt-5">
            <div class="text-center flex w-[400px] h-[30px] bg-gray-700 border border-blue-600 mx-auto ">
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-8 h-8 p-2 text-white">
                 <path stroke-linecap="round" stroke-linejoin="round" d="M21 21l-5.197-5.197m0 0A7.5 7.5 0 105.196 5.196a7.5 7.5 0 0010.607 10.607z" />
                </svg>
                <input type="text"  class="bg-transparent mx-auto focus:none  focus:outline-none" placeholder="Search...">
            </div>
        <div v-for="todo in todoList" :key="todo.text" class="justify-between flex w-[400px] h-[30px] bg-white border border-blue-600   mx-auto mt-5">
                <ul class="list-disc ml-3">
                    <li v-if="todo.completed" class="ml-3 text-green-500">{{ todo.text }}</li>
                    <li v-else class="ml-3 text-gray-500">{{ todo.text }}</li>
                </ul>
            <div class="flex">
               
                <button @click="editLi(todo)">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6 mr-2 text-blue-500">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M16.862 4.487l1.687-1.688a1.875 1.875 0 112.652 2.652L6.832 19.82a4.5 4.5 0 01-1.897 1.13l-2.685.8.8-2.685a4.5 4.5 0 011.13-1.897L16.863 4.487zm0 0L19.5 7.125" />
                    </svg>
                </button>
                <button @click="deleteTodo(todo)" class="mr-3">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6 text-red-600">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M20.25 7.5l-.625 10.632a2.25 2.25 0 01-2.247 2.118H6.622a2.25 2.25 0 01-2.247-2.118L3.75 7.5M10 11.25h4M3.375 7.5h17.25c.621 0 1.125-.504 1.125-1.125v-1.5c0-.621-.504-1.125-1.125-1.125H3.375c-.621 0-1.125.504-1.125 1.125v1.5c0 .621.504 1.125 1.125 1.125z" />
                    </svg>
                </button>
                <button v-if="!todo.completed"  @click="completeLi(todo)" class="pr-3">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6 hover:text-green-500">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M9 12.75L11.25 15 15 9.75m-3-7.036A11.959 11.959 0 013.598 6 11.99 11.99 0 003 9.749c0 5.592 3.824 10.29 9 11.623 5.176-1.332 9-6.03 9-11.622 0-1.31-.21-2.571-.598-3.751h-.152c-3.196 0-6.1-1.248-8.25-3.285z" />
                    </svg>
                </button>
            </div>
        </div>
           <div @click="dialog=true || false" class=" w-[400px] h-[30px]  bg-gray-700 border border-black hover:border-blue-500         text-center mx-auto mt-5">
                <button   class="text-white ">Add New todo...</button>
            </div>
        </div>
         <div>
            <dialog :open="dialog" class="w-[400px] h-auto position:absolute ">
            <input type="text"  v-model="todo" placeholder="Create todo type..."  class=" w-[400px] h-[30px]  bg-gray-700 border border-black hover:border-blue-500 text-center mx-auto mt-5"/><br>
            <button v-if="!editing" @click="addTodo()" class="mr-9 px-4 py-1 bg-gray-700 border border-black hover:border-blue-500 text-center mx-auto mt-5"> Save</button>
            <button v-else @click="updateLi()" class=" mr-9 px-4 py-1 bg-gray-700 border border-black hover:border-blue-500 text-center mx-auto mt-5">update</button>
            <button @click="cancel()" class=" mr-9 px-4 py-1 bg-gray-700 border border-black hover:border-blue-500 text-center mx-auto mt-5">Cancel</button>
        
            </dialog>
        </div>
    </section>
</template>

<!----------------script--------------------->
<script>
export default{
    data(){
        return{
            todo:'',
            todoList:[],
            dialog:false,
            editing:false,
            store:{}
        }
    },
    methods:{
        addTodo(){
            this.dialog=true
            let id = new Date().getTime()
            this.todoList.push(
                {text:this.todo, completed:false, id: id}
            )
            this.dialog=false
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
        },
        cancel(){
            this.dialog=false;
            this.todo='';
            this.editing=false
        },
        editLi(todo){
           this.todo=todo.text
           this.dialog=true
           this.editing=true
           this.store=todo
        },
        updateLi(){
            let index=this.todoList.indexOf(this.store)
            this.todoList.splice(index,1)
            this.todoList.push(
                {text:this.todo, completed:false}
            )
            this.cancel()
        }
        
    }
}
</script>