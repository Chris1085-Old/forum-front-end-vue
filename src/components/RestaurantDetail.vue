<template>
  <div class="row">
    <div class="col-md-12 mb-3">
      <h1>{{ restaurant.id }} {{ restaurant.name }}</h1>
      <p class="badge bg-secondary mt-1 mb-3">
        {{ restaurant.categoryName }}
      </p>
    </div>
    <div class="col-lg-4">
      <img
        class="img-responsive center-block"
        :src="restaurant.image"
        style="width: 250px;margin-bottom: 25px;"
      />
      <div class="contact-info-wrap">
        <ul class="list-unstyled">
          <li>
            <strong>Opening Hour:</strong>
            {{ restaurant.openingHours }}
          </li>
          <li>
            <strong>Tel:</strong>
            {{ restaurant.tel }}
          </li>
          <li>
            <strong>Address:</strong>
            {{ restaurant.address }}
          </li>
        </ul>
      </div>
    </div>
    <div class="col-lg-8">
      <p>{{ restaurant.description }}</p>
      <router-link
        :to="`/restaurants/${restaurant.id}/dashboard`"
        class="btn btn-primary btn-border mr-2"
        >Dashboard</router-link
      >

      <button
        v-if="restaurant.isFavorited"
        type="button"
        class="btn btn-danger btn-border favorite mr-2"
        @click.stop.prevent="favoriteToggle"
      >
        移除最愛
      </button>
      <button
        v-else
        type="button"
        class="btn btn-primary btn-border favorite mr-2"
        @click.stop.prevent="favoriteToggle"
      >
        加到最愛
      </button>
      <button
        v-if="restaurant.isLiked"
        type="button"
        class="btn btn-danger like mr-2"
        @click.stop.prevent="likeToggle"
      >
        Unlike
      </button>
      <button
        v-else
        type="button"
        class="btn btn-primary like mr-2"
        @click.stop.prevent="likeToggle"
      >
        Like
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    initialRestaurant: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      restaurant: this.initialRestaurant
    }
  },
  methods: {
    favoriteToggle() {
      this.restaurant.isFavorited = !this.restaurant.isFavorited
    },
    likeToggle() {
      this.restaurant.isLiked = !this.restaurant.isLiked
    }
  }
}
</script>
