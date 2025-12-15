<template>
  <div id="app">
    <!-- Toast component -->
    <ToastService ref="toastService" />
    
    <div class="hero"></div>

    <div class="content">
      <h1>Our Collection</h1>
      <p>Introducing our Coffee Collection, a selection of unique coffees from different roast types and origins, expertly roasted in small batches and shipped fresh weekly.</p>

      <!-- Updated button container -->
      <div class="button-container">
        <Button 
          class="CoffeeBtn"
          :class="{ active: activeTab === 'all' }"
          label="All Products"
          @click="activeTab = 'all'"
        />

        <Button 
          class="CoffeeBtn"
          :class="{ active: activeTab === 'available' }"
          label="Available Now"
          severity="secondary"
          text
          @click="activeTab = 'available'"
        />
      </div>

      <!-- Use ReusableCards component -->
      <ReusableCards :filteredCoffees="filteredCoffees" />
    </div>
  </div>
</template>
<script>
import Button from 'primevue/button';
import ToastService from './components/ToastService.vue';
import ReusableCards from './components/ReusableCards.vue';

export default {
  name: 'App',
  components: {
    ReusableCards,
    ToastService,
    Button
  },
  data() {
    return {
      activeTab: 'all',
      coffees: []
    };
  },
  computed: {
    filteredCoffees() {
      if (this.activeTab === 'available') {
        return this.coffees.filter(coffee => coffee.available);
      }
      return this.coffees;
    }
  },
  created() {
    this.getCoffees();
  },
  methods: {
    getCoffees() {
      fetch(
        "https://raw.githubusercontent.com/devchallenges-io/curriculum/refs/heads/main/4-frontend-libaries/challenges/group_1/data/simple-coffee-listing-data.json"
      )
        .then(response => {
          if (!response.ok) {
            throw new Error('Network response was not ok');
          }
          return response.json();
        })
        .then(data => {
          this.coffees = data;

          // Toast success
          this.$refs.toastService.showSuccess(
            `Loaded ${this.coffees.length} coffee products successfully!`
          );
        })
        .catch(error => {
          console.error(error);

          // Toast error
          this.$refs.toastService.showError(
            'Failed to load coffee products. Please try again.'
          );
        });
    }
  },
  watch: {
    activeTab(newTab) {
      if (newTab === 'available') {
        const count = this.coffees.filter(c => c.available).length;
        this.$refs.toastService.showInfo(`Showing ${count} available products`);
      } else {
        this.$refs.toastService.showInfo(`Showing all ${this.coffees.length} products`);
      }
    }
  }
};
</script>


<style>
* {
  margin: 0;
  padding: 0;
}

body {
  background-color: #121315;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

.hero {
  width: 100%;
  height: 50vh;
  background-image: linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)), url("/hero-bg.jpg");
  background-size: cover;
  background-position: top;
  background-repeat: no-repeat;
  display: flex;
  justify-content: center;
  align-items: center;
}

.content {
  padding: 20px;
  color: white;
  width: 80%;
  margin: 0 auto;
  text-align: center;
  margin-top: -100px;
  z-index: 1;
  background-color: #1c1d1f;
  border-radius: 10px;
  margin-bottom: 50px;
}

/* Mobile (default - under 768px) */
.content p {
  width: 90%;
  margin: 0 auto;
  text-align: center;
  line-height: 1.6;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
}

.content h1 {
  font-size: 1.8em;
  margin-top: 20px;
  margin-bottom: 20px;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  font-weight: 600;
}

/* Small mobile (optional extra small screens) */
@media (max-width: 480px) {
  .content p {
    width: 95%;
    font-size: 0.95em;
    line-height: 1.5;
  }
  
  .content h1 {
    font-size: 1.6em;
    margin-top: 15px;
    margin-bottom: 15px;
  }
}

/* Tablet and up (768px and above) */
@media (min-width: 768px) {
  .content p {
    width: 85%;
    font-size: 1em;
    line-height: 1.6;
  }
  
  .content h1 {
    font-size: 2.2em;
  }
}

/* Desktop and up (1024px and above) */
@media (min-width: 1024px) {
  .content p {
    width: 70%;
  }
  
  .content h1 {
    font-size: 2.5em;
  }
}

/* Large desktop (1280px and above) */
@media (min-width: 1280px) {
  .content p {
    width: 50%;
  }
  
  .content h1 {
    font-size: 2.8em;
  }
}

/* Extra large screens (optional) */
@media (min-width: 1536px) {
  .content p {
    width: 50%;
    max-width: 800px;
  }
  
  .content h1 {
    font-size: 3em;
  }
}

.button-container {
  display: flex;
  justify-content: center;
  gap: 12px;
  margin: 30px 0;
}

.CoffeeBtn {
  width: 160px !important;
  height: 45px !important;
  padding: 0 !important;
  border-radius: 6px !important;
  font-weight: 600 !important;
  transition: 0.2s;
  display: flex;
  justify-content: center;
  align-items: center;
}

.CoffeeBtn.active {
  background-color: #c49a6c !important;
  color: #1c1d1f !important;
  border: none !important;
}

.CoffeeBtn:not(.active) {
  background-color: transparent !important;
  color: #c49a6c !important;
  border: none !important;
}

.CoffeeBtn:not(.active):hover {
  background-color: rgba(196,154,108,0.2);
  backdrop-filter: blur(6px);
  -webkit-backdrop-filter: blur(6px);
  color: #c49a6c !important;
  transform: translateY(-1px);
  cursor: pointer;
}

.p-toast {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
}

.p-toast .p-toast-message {
  border-radius: 8px;
  margin: 10px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}
</style>