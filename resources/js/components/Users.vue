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
                      <th>Modify</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr>
                      <td>183</td>
                      <td>John Doe</td>
                      <td>11-7-2014</td>
                      <td>Approved</td>
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

  <div class="form-group">
    <div class="form-group">
    <input id="username" v-model="form.name" type="text" name="name" placeholder="Name"
     class="form-control" :class="{ 'is-invalid' : form.errors.has('name')}" >
    <HasError :form="form" field="username" />
  </div>
<div class="form-group">
    <input id="email" v-model="form.email" type="email" name="name"
     placeholder="Email"
     class="form-control" :class="{ 'is-invalid' : form.errors.has('name')}" >
    <HasError :form="form" field="username" />
  </div>
       
       <div class="form-group">
    <input id="password" v-model="form.password" type="text" name="name" 
    placeholder="Password"
     class="form-control" :class="{ 'is-invalid' : form.errors.has('name')}" >
    <HasError :form="form" field="username" />
  </div>

      </div></div>
      <div class="modal-footer">
        <button type="button" class="btn btn-danger" data-bs-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary">create</button>
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
        mounted() {
            console.log('Component mounted.')
        }
    }
</script>
