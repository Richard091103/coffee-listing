<template>
  <div class="coffee-list">
    <Card 
      class="CoffeeCard" 
      v-for="coffee in filteredCoffees" 
      :key="coffee.name"
    >
      <template #header>
        <div class="coffee-img-wrapper">
          <!-- Image tag if popular -->
          <span v-if="coffee.popular" class="popular-label">Popular</span>
          <img 
            :src="coffee.image" 
            alt="Coffee Image" 
            class="coffee-img" 
          />
        </div>
      </template>

      <template #title>
        <div class="coffee-info">
          <span class="coffee-title">{{ coffee.name }}</span>
          <span class="coffee-price">
            {{ coffee.price }}
          </span>
        </div>
      </template>

      <template #content>
        <div class="coffee-info-bottom">
          <div class="coffee-rating">
            <span class="rate">
              <!-- Empty star when no votes -->
              <img 
                v-if="coffee.votes === 0" 
                src="@/assets/Star.svg" 
                alt="Empty Star" 
                class="star-icon" 
              />
              <!-- Filled star otherwise -->
              <img 
                v-else 
                src="@/assets/Star_fill.svg" 
                alt="Star" 
                class="star-icon" 
              />

              
              <span v-if="coffee.rating !== null">
                {{ coffee.rating }}
              </span>

              <!-- If the rating is null, show "No Rating" -->
              <span v-else class="no-rating">
                No Rating
              </span>
            </span>

            <!-- Votes -->
            <!-- Only show votes if there are votes -->
            <span v-if="coffee.votes > 0" class="votes">({{ coffee.votes }} votes)</span>
            <!-- Show "No ratings" text for 0 votes -->
            <span v-else class="no-votes">(0 votes)</span>
          </div>


          <div class="coffee-availability">
            <span :class="coffee.available ? 'available' : 'unavailable'">
              {{ coffee.available ? 'Available' : 'Out of stock' }}
            </span>
          </div>
        </div>
      </template>
    </Card>
  </div>
</template>

<script>
import Card from 'primevue/card';

export default {
  name: "CoffeeManager",
  components: { Card },
  props: {
    filteredCoffees: {
      type: Array,
      default: () => []
    }
  }
};
</script>


<style>
.coffee-list {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
  margin-top: 20px;
}

.CoffeeCard {
  background: transparent !important;
  box-shadow: none !important;
  border: none !important;
  transition: transform 0.2s;
  width: 100% !important;
  margin: 0 !important;
}

.CoffeeCard:hover {
  transform: translateY(-4px);
}

.coffee-img-wrapper {
  position: relative;
  width: 100%;
  height: 180px;
  overflow: hidden;
}

.coffee-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-bottom: 1px solid rgba(0,0,0,0.1);
  border-radius: 10px;
}

.popular-label {
  position: absolute;
  top: 10px;
  left: 10px;
  background-color: #ffd000;
  color: #1c1d1f;
  padding: 4px 20px;
  border-radius: 50px;
  font-size: 0.85em;
  font-weight: bold;
  box-shadow: 0 2px 6px rgba(0,0,0,0.2);
  z-index: 2;
}

.coffee-info {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 10px;
}

.coffee-title {
  font-size: 1.2rem;
  font-weight: 700;
  color: #f5b82a;
}

.coffee-price {
  font-size: 1rem;
  color: #333333;
  background-color: #bee3cc;
  padding: 4px 10px;
  border-radius: 6px;
}

.coffee-info-bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 10px;
}

.coffee-rating {
  display: flex;
  align-items: center;
  font-size: 0.9rem;
  color: #ffffff;
  font-weight: bold;
}

.star-icon {
  width: 20px;
  height: 20px;
  margin-right: 4px;
  display: inline-block;
  vertical-align: middle;
}

.rate {
  display: flex;
  align-items: center;
  margin-right: 6px;
}

.votes {
  color: #666;
  margin-left: 4px;
}

.no-votes {
  color: #999;
  margin-left: 4px;
  font-size: 0.85rem;
}

.coffee-availability {
  font-size: 0.9rem;
}

.available {
  color: #28a745;
  font-weight: 600;
}

.unavailable {
  color: #dc3545;
  font-weight: 600;
}

/* Responsive styles */
@media (max-width: 1024px) {
  .coffee-list {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 640px) {
  .coffee-list {
    grid-template-columns: 1fr;
  }
}
</style>