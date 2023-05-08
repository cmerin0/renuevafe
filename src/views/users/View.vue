<template>
    <div class="container">
        <div class="card mt-3">
            <div class="card-header">
                <h4 class="card-title float-start">Users</h4>
                <RouterLink to="/users/create" class="btn btn-success float-end">Add User</RouterLink>
            </div>
            <div class="card-body">
                <table class="table table-bordered">
                    <thead>
                        <tr>
                            <th>ID</th>
                            <th>Username</th>
                            <th>Password</th>
                            <th>E-Mail</th>
                            <th>User Type</th>
                            <th>Operations</th>
                        </tr>
                    </thead>
                    <tbody v-if="this.users.length > 0">
                        <tr v-for="(user, index) in this.users" :key="index">
                            <td>{{ user.id_user }}</td>
                            <td>{{ user.username }}</td>
                            <td>{{ user.password }}</td>
                            <td>{{ user.email }}</td>
                            <td>{{ user.id_type_user }}</td>
                            <td>
                                <RouterLink :to="{ path: '/users/' + user.id_user + '/edit' }" class="btn btn-warning ms-2">Update</RouterLink>
                                <button type="button" @click="deleteUser(user.id_user)" class="btn btn-danger ms-2">Delete</button>
                            </td>
                        </tr>
                    </tbody>
                    <tbody v-else><tr><td colspan="6"><h3>Loading...</h3></td></tr></tbody>
                </table>
            </div>
        </div>
    </div>
</template>
  
<script>
    import axios from 'axios' 
    export default {
        name: 'users',
        data() {
            return {
                users: []
            }
        },
        mounted() {
            this.getUsers()
        },
        methods: {
            getUsers() {
                axios.get('http://localhost:3300/api/users').then(res => { this.users = res.data })
            }, 
            deleteUser(id_user){
                if (confirm('Are you sure of deleting this user?')){
                    axios.delete('http://localhost:3300/api/users/' + id_user).then(res => {
                        alert(res.data)
                        this.getUsers()
                    })
                }
            }
        }
    }
</script>
  <style>
  </style>
  