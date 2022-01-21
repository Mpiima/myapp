<template>
    <div class="container">
         <!-- /.row -->
        <div class="row mt-5">
          <div class="col-md-12">
            <div class="card">
              <div class="card-header">
                <h3 class="card-title">User List</h3>

                <div class="card-tools">
                  <button class="btn btn-success" data-bs-toggle="modal" data-bs-target="#adduser">Add New <i class="fas fa-user-plus"></i></button>
                </div>
              </div>
              <!-- /.card-header -->
              <div class="card-body table-responsive p-0">
                <table class="table table-hover text-nowrap">
                  <thead>
                    <tr>
                      <th>ID</th>
                      <th>Name</th>
                      <th>Email</th>
                      <th>Type</th>
                      <th>Registered on</th>
                      <th>Modify</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="user in users" :key="user.id">
                      <td>{{user.id}}</td>
                      <td>{{user.name}}</td>
                      <td>{{user.email}}</td>
                      <td>{{user.type | capitalize}}</td>
                      <td>{{user.created_at | myDate}}</td>
                      <td>
                          <i class="fas fa-edit blue"></i>
                           <i class="fas fa-trash red"></i>
                      </td>
                    </tr>
                  </tbody>
                </table>
              </div>
              <!-- /.card-body -->
            </div>
            <!-- /.card -->
          </div>
        </div>
        <!-- /.row -->
        <!-- Modal -->
<div class="modal fade" id="adduser" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog modal-dialog-centered">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="adduserLabel">Add New</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">


<form @submit.prevent="createUser">
   <div class="form-group">
    <input v-model="form.name" type="text" name="name" placeholder="Name" class="form-control">
    <div v-if="form.errors.has('name')" v-html="form.errors.get('name')" />
    </div>
    <div class="form-group">
    <input v-model="form.email" type="text" name="type" placeholder="Email" class="form-control">
    <div v-if="form.errors.has('email')" v-html="form.errors.get('email')" />
      </div>
      
       <div class="form-group">
    <textarea v-model="form.bio"  name="bio" placeholder="Short bio for user(Optional)" class="form-control">
    </textarea>
    <div v-if="form.errors.has('bio')" v-html="form.errors.get('bio')" />
      </div>

       <div class="form-group">
    <select v-model="form.type"  name="type" placeholder="Short bio for user(Optional)" class="form-control">
      <option value="">Select User Role</option>
      <option value="admin">Admin</option>
      <option value="user">Standard User</option>
      <option value="author">Author</option>
    </select>
    <div v-if="form.errors.has('type')" v-html="form.errors.get('type')" />
      </div>
    
    <div class="form-group">
    <input v-model="form.password" type="password" name="password" placeholder="password" class="form-control">
    <div v-if="form.errors.has('password')" v-html="form.errors.get('password')" />
      </div>

      <div class="modal-footer">
        <button type="button" class="btn btn-danger" data-bs-dismiss="modal">Close</button>
        <button type="submit" class="btn btn-primary">create</button>
      </div>
    </form>
    </div>
    </div>
  </div>
</div>
    </div>
</template>

<script>
    export default {
        data(){
        return{
          users : {},
         form:new Form(
             {
                 name : '',
                 email : '',
                 password: '',
                 type: '',
                 bio: '',
                 photo:''
             }
         )
        }
        },
          methods: {
     loadUsers(){
         axios.get("api/user").then(({ data }) => (this.users = data.data));
            },
   createUser(){
    this.$Progress.start();
     this.form.post('api/user');
     this.$Progress.finish()
   }
  },
        created() {
            this.loadUsers();
        }
    }
</script>
