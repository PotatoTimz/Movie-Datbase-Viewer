<template>
    <div class="has-text-white has-background-dark">
        <br><text id="welcome">Your Profile</text><br>
        <br><br>
    </div>
    <div class="container is-fluid ">
        <div class="columns is-multiline">
            <div id="information">
            <h1><strong id="information_header">Personal Information</strong></h1><br>
                <div v-if="!editingName">
                    <strong>Name:</strong> {{ fullName }}
                    <button id="edit_button" class="mr-5 button is-small is-dark is-outlined" @click="startEditing('name')">Edit</button>
                </div>
                <div class="field is-horizontal" v-if="editingName">
                    <label id="info_labels" class="has-text-weight-bold" for="fullName">Name:</label>
                    <input class="input is-dark" type="text" placeholder="Name" id="fullName" v-model="fullNameEdit" />
                    <button id="save_button" class="button is-small is-info" @click="saveProfile('name')">Save</button>
                    <button id="cancel_button" class="button is-small is-dark is-outlined" @click="cancelEditing('name')">Cancel</button>
                </div><br>
                <div v-if="!editingEmail">
                    <strong>Email:</strong> {{ email }}
                    <button id="edit_button" class="button is-small is-dark is-outlined" @click="startEditing('email')">Edit</button>
                </div>
                <div class="field is-horizontal" v-if="editingEmail">
                    <label id="info_labels" class="has-text-weight-bold" for="email">Email:</label>
                    <input class="input is-dark" type="email" placeholder="Email" id="email" v-model="emailEdit" />
                    <button id="save_button" class="button is-small is-info" @click="saveProfile('email')">Save</button>
                    <button id="cancel_button" class="button is-small is-dark is-outlined" @click="cancelEditing('email')">Cancel</button>
                </div><br>
                <div v-if="!editingPhone">
                    <strong>Phone:</strong> {{ phone }}
                    <button id="edit_button" class="button is-small is-dark is-outlined" @click="startEditing('phone')">Edit</button>
                </div>
                <div class="field is-horizontal" v-if="editingPhone">
                    <label id="info_labels" class="has-text-weight-bold" for="phone">Phone:</label>
                    <input class="input is-dark" type="tel" placeholder="Phone" id="phone" v-model="phoneEdit" />
                    <button id="save_button" class="button is-small is-info" @click="saveProfile('phone')">Save</button>
                    <button id="cancel_button" class="button is-small is-dark is-outlined" @click="cancelEditing('phone')">Cancel</button>
                </div><br>
                <div v-if="!editingAddress">
                    <strong>City:</strong> {{ address }}
                    <button id="edit_button" class="button is-small is-dark is-outlined" @click="startEditing('address')">Edit</button>
                </div>
                <div class="field is-horizontal" v-if="editingAddress">
                    <label id="info_labels" class="has-text-weight-bold" for="address">City:</label>
                    <textarea class="input is-dark" placeholder="City" id="address" v-model="addressEdit"></textarea>
                    <button id="save_button" class="button is-small is-info" @click="saveProfile('address')">Save</button>
                    <button id="cancel_button" class="button is-small is-dark is-outlined" @click="cancelEditing('address')">Cancel</button>
                </div>
        
            </div>
        </div>
    </div>
    

    
    <h1><strong class="has-text-info" id="movie_list_header">My Movie List ❤</strong></h1><br>
    <div class="container is-fluid has-background-dark">
        <div class="columns is-multiline">
            <div v-for="(movie, index) in movieList" v-bind:key="index" id="movie_list">
                <img class="is-clickable" v-bind:src="movie.poster" v-on:click="moreInfo(movie.id)" id="poster">
            </div>
        </div>
    </div>
     

    
  </template>
  
  <script>
  export default {
    name: 'ProfilePage',
    data() {
        return {
            userName: 'Demo',
            fullName: 'Demo',
            fullNameEdit: '',
            editingName: false,
            email: 'demo@gmail.com',
            emailEdit: '',
            editingEmail: false,
            phone: '905-123-1234',
            phoneEdit: '',
            editingPhone: false,
            address: 'Oshawa, ON',
            addressEdit: '',
            editingAddress: false,
            movieList: [],
            title: ""
        }
    },
    async mounted(){
            const res = await fetch("https://api.themoviedb.org/3/trending/all/day?api_key=b9dfda1d995db256a3b3ae948d044866")
            const movieInfo = await res.json();
            console.log(movieInfo.results[0].title);
            this.title = movieInfo.results[0].title;
    
            console.log(this.title);
            for(let i = 0; i < 10; i++){
                this.movieList.push({id:movieInfo.results[i].id, title: movieInfo.results[i].title, poster: "https://image.tmdb.org/t/p/original/"+movieInfo.results[i].poster_path});
            }
        },
    methods: {
        startEditing(field) {
            if (field === 'name') {
                this.fullNameEdit = this.fullName;
                this.editingName = true;
            } else if (field === 'email') {
                this.emailEdit = this.email;
                this.editingEmail = true;
            } else if (field === 'phone') {
                this.phoneEdit = this.phone;
                this.editingPhone = true;
            } else if (field === 'address') {
                this.addressEdit = this.address;
                this.editingAddress = true;
            }
        },
        saveProfile(field) {
            if (field === 'name') {
                this.fullName = this.fullNameEdit;
                this.editingName = false;
            } else if (field === 'email') {
                this.email = this.emailEdit;
                this.editingEmail = false;
            } else if (field === 'phone') {
                this.phone = this.phoneEdit;
                this.editingPhone = false;
            } else if (field === 'address') {
                this.address = this.addressEdit;
                this.editingAddress = false;
            }
        },
        cancelEditing(field) {
            if (field === 'name') {
                this.editingName = false;
            } else if (field === 'email') {
                this.editingEmail = false;
            } else if (field === 'phone') {
                this.editingPhone = false;
            } else if (field === 'address') {
                this.editingAddress = false;
            }
        },
        moreInfo(movieID){
                this.$emit("selected", movieID);
            }
    }
  };
  </script>
  
  <style>

    #welcome{
        font-size: 40px;
        margin: 4rem;
        }
    #message{
        font-size: 30px;
        margin: 4rem;
    }
    #information_header{
        font-size: 30px;
    }
    #information{
        font-size: 20px;
        margin-top: 4rem;
        margin-left: 3rem;
        margin-bottom: 5rem;
    }
    #edit_button{
        margin-right: 10rem;
    }
    #save_button{
        margin-left: 5rem;
    }
    #cancel_button{
        
        margin-left: 1rem;
    }
    #info_labels{
        margin-right: 1rem;
    }
    #movie_list_header{
        margin-top: 10rem;
        margin-left: 4rem;
        font-size: 30px;
    }
    #movie_list{
        margin-left: 3rem;
        margin-right: 4rem;
        margin-bottom: 4rem;
        margin-top: 4rem;
    }
    #poster_border{
        margin-right: 4rem;
    }
    #poster{
        height: 20rem;
        width: 15rem;
        border: 4px solid rgb(50, 134, 230);
    }
    #poster:hover{
        border: 4px solid rgb(255, 255, 255);
    }

  </style>
  