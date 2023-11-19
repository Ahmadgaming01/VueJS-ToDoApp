<template>
    <div class="container my-5">
        <div class="row">
            <div class="col-lg-6 mx-auto">
                <h3 class="my-4 text-center">ToDo App</h3>
                <div class="d-flex">
                    <input type="text" class="form-control w-100 " placeholder="Enter your Task">
                    <button class="btn btn-warning rounded ms-3">Add New Task</button>
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
                        <tr v-for = " (name , index) in tasks " :key="index">
                        <td>{{ name.task }}</td>
                        <td>Witing</td>
                        <td><div>
                            <a href="#"><span class="fa fa-edit"></span></a>
                            
                        </div></td>
                        <td><div>
                            
                            <a href="#"><span class="fa fa-times"></span></a>
                        </div></td>
                        </tr>

                    </tbody>
                    </table>

                            </div>
                        </div>
</template>


<script>

export default {
    name: "HelloWorld",
    data(){
        return{
            tasks:[
                {task:"study js",status:'waiting'},
                {task:"study css",status:'done'}
            ],
        }
    }

}
</script>