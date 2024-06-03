<template>
  <section id="Review">
    <section class="hero is-dark">
      <!-- Existing code -->
    </section>
    <section class="section">
      <div class="container">
        <h2 class="title">Add a Review</h2>
        <form @submit.prevent="submitReview">
          <div class="field">
            <label class="label">Name</label>
            <div class="control">
              <textarea v-model="Name" class="textarea" required></textarea>
            </div>
          </div>
          <div class="field">
            <label class="label"> Movie name</label>
            <div class="control">
              <textarea v-model="moviename" class="textarea" required></textarea>
            </div>
          </div>
          <div class="field">
            <label class="label">Review</label>
            <div class="control">
              <textarea v-model="Review" class="textarea" required></textarea>
            </div>
          </div>
          <div class="field">
            <div class="control">
              <button type="submit" class="button is-primary">Submit Review</button>
            </div>
          </div>
          <div class="reviews">
          <h2>Reviews</h2>
          <ul>
            <li v-for="review in reviews" :key="review.id">
              <p><strong>{{ review.Name }}  {{ review.moviename}}</strong></p>
              <p> {{ review.Review}}</p>
            </li>
          </ul>
        </div>
        </form>
      </div>
    </section>
  </section>
</template>

<script>
export default {
  name: "ReviewPage",
  data() {
    return {
      Name: "",
      moviename:"",
      Review: "",
      reviews: [],
    };
  },
  methods: {
    submitReview() {
      if (this.Name  && this.Review) {
        const review = {
          Name: this.Name,
          moviename: this.moviename,
          Review: this.Review,
        };
        this.reviews.push(review);
        this.Name = "";
        this.moviename = "";
        this.Review = "";
      }
    },
  },
};
</script>
