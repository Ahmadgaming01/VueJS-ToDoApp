<template>
    <div class="container my-5">
        <div class="row">
            <div class="col-lg-6 mx-auto">
                <h3 class="my-4 text-center">ToDo App</h3>
                <div class="d-flex">
                    <input type="text" v-model="new_task" class="form-control w-100 " placeholder="Enter your Task">
                    <button class="btn btn-warning rounded ms-3" @click="addTask" >Add New Task</button>
            </div>
                    </div>
                    <table class="table mt-5">
                    <thead>
                        <tr>

                        <th scope="col">Task</th>
                        <th scope="col">Status</th>
                        <th scope="col">Edit</th>
                        <th scope="col">Delete</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for = " (task , index) in tasks " :key="index">
                        <td>{{ task.name }}</td>
                        <td>{{ task.status }}</td>
                        <td><div @click="editTask(index)">
                            <a href="#"><span class="fa fa-edit"></span></a>
                            
                        </div></td>
                        <td>
                            <div @click ="deleteTask(index)">
                                <span class="fa fa-times"></span>
                            </div>
                        </td>
                        </tr>

                    </tbody>
                    </table>

                            </div>
                        </div>
</template>


<script>
import { toast } from 'vue3-toastify';
import 'vue3-toastify/dist/index.css';
import axios from "axios"

export default {
    name: "HelloWorld",
    data(){
        return{
            tasks:[],
            new_task:"",
            edited_task:null,
        }
    },
    mounted(){
        this.getTodo()

        
    },
    methods:{
        getTodo(){
            axios({
                method: 'get',
                url: 'http://localhost:8000/todo/'

            }).then(
                response => {
                    this.tasks = response.data
                }
            )
        },
        
        addTask(){
            if (this.new_task == 0) return;


            if (this.edited_task==null){
                this.tasks.push({task:this.new_task,status:'waiting'})
                this.new_task = ""
                toast.success('New task was added successfully !',{
                autoClose: 2000,
            }); 
            }
            else{
                this.tasks[this.edited_task].task=this.new_task
                this.edited_task=null
                this.new_task=""
                toast.success('task was updated successfully !',{
                autoClose: 2000,
            });
            }
        },
        deleteTask (index){
            this.tasks.splice (index , 1) // (1) to delete one item
            toast.error('task was deleted successfully !',{
            autoClose: 2000,
            });
        },
        editTask(index){
            this.new_task = this.tasks[index].task
            this.edited_task= index;
            
        },

    },

}
</script>