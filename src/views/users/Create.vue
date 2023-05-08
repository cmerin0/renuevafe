<template>
    <div class="container">
        <div class="card mt-3">
            <h4 class="card-header">Add User</h4>
            <div class="card-body">
                <form>
                    <div class="mb-3">
                        <label for="exampleInputUsername" class="form-label">Username</label>
                        <input type="text" v-model="model.user.username" class="form-control" id="exampleInputUsername">
                    </div>
                    <div class="mb-3">
                        <label for="exampleInputPassword1" class="form-label">Password</label>
                        <input type="password" v-model="model.user.password" class="form-control" id="exampleInputPassword1">
                    </div>
                    <div class="mb-3">
                        <label for="exampleInputEmail1" class="form-label">E-Mail</label>
                        <input type="email" v-model="model.user.email" class="form-control" id="exampleInputEmail1">
                    </div>
                    <button type="button" @click="saveUser" class="btn btn-primary">Save</button>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from 'axios'
    export default {
        name: 'userCreate',
        data() {
            return {
                model: {
                    user: {
                        username: '',
                        password: '',
                        email: '',
                        id_type_user: 2,
                    }
                }
            }
        },
        methods: {
            saveUser(){
                axios.post('http://localhost:3300/api/users', this.model.user).then(res => {
                    console.log(res.data)
                    this.model.user = {
                        username: '',
                        password: '',
                        email: '',
                        id_type_user: 2,
                    }
                    if(res.status === 201) this.$router.push('/users')
                }).catch(function(e){
                    console.error(e) // here we handle errors according to backend
                })
            }
        }
    }
</script>