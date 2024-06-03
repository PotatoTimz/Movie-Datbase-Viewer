<template>
    <section id="Ratings">
      <section class = "hero is-dark">
      <div id ="info">
    <h1 class = "title">Information on the personnel</h1>
   
        <div class="column is-3">
                  <img v-bind:src="profile_path">
              </div>
        <p><strong>Name: </strong>{{ name }}</p>
        <p><strong>Biography: </strong>{{ biography }}</p>
        <p><strong>Birthday: </strong>{{ birthday }}</p>
        <p><strong>Birthplace: </strong>{{ place_of_birth }}</p>

      </div>
</section>
    </section>
  </template>

<script>


 export default {
  name: "RatingsPage",
  props: {
      id: String
    },
  data(){
    return{
    personID: this.id,
    biography: "",
    birthday: "",
    name: "",
    place_of_birth: "",
    profile_path: "",
    


    }
  },
  async mounted(){
    console.log(this.personID)
    const res = await fetch("https://api.themoviedb.org/3/person/"+this.personID+"?api_key=b9dfda1d995db256a3b3ae948d044866")
    const personInfo = await res.json();
    this.biography = personInfo.biography;
    this.birthday= personInfo.birthday;
    this.name= personInfo.name;
    this.place_of_birth = personInfo.place_of_birth;
    this.profile_path = "https://image.tmdb.org/t/p/original/" + personInfo.profile_path
    console.log(personInfo)
    console.log(personInfo.place_of_birth)

  
    if (personInfo.name===""){
      this.name = "There is no available information for this field."

    }

    if (personInfo.biography===""){
      this.biography = "There is no available information for this field."
    }
    if (personInfo.birthday===null){
      this.birthday = "There is no available information for this field."
    }
    if (personInfo.place_of_birth===null){
      this.place_of_birth = "There is no available information for this field."
    }

    if (personInfo.profile_path===null){
      console.log("No profile picture")
      this.profile_path = "silhouette.png";
    }
    

  
  
  
  

 }//end async fetch


 
 }
 
</script>

