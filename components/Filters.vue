<template>
  <div class="filters">
    <div class="filters">
      <section class="filter-section">
        <form class="filter-form" @submit="submited">
          <div class="filter">
            <p class="filter-label">destinations</p>
            <select v-model="form.city" class="filter-select">
                <option value disabled selected>Select Your Favorite Cities</option>
              <option value="All" class="filter-option">All</option>
              <option v-for="(city, index) in cities" :key="index" :value="city.name" class="filter-option">{{city.name}}</option>
            </select>
          </div>
          <div class="filter">
            <p class="filter-label">duration</p>
            <select
                v-model="form.days"
              class="filter-select"
            >
              <option value disabled selected>How Long ?</option>
              <option value="all" class="filter-option">All</option>
              <option value="1" class="filter-option">One Week</option>
              <option value="2" class="filter-option">Two Week</option>
              <option value="3" class="filter-option">One Month</option>
            </select>
          </div>
          <div class="pair-select">
            <div class="filter">
              <p class="filter-label">budget range</p>
              <select
                v-model="form.budget"
                class="filter-select"
              >
                <option value disabled selected>How Much ?</option>
                <option value="all" class="filter-option">All</option>
                <option value="1" class="filter-option">Tight Budget</option>
                <option value="2" class="filter-option">Mid Budget</option>
                <option value="3" class="filter-option">Luxury Budget</option>
              </select>
            </div>
            <div class="filter">
              <p class="filter-label">travelers</p>
              <select id="travelers" name="travelers" class="filter-select">
                <option value disabled selected>How Many Guys?</option>
                <option name="all" class="filter-option">All</option>
                <option name="one" class="filter-option">1 Passenger</option>
                <option value="two" class="filter-option">2 Passenger</option>
                <option value="three" class="filter-option">3 Passenger</option>
                <option value="four" class="filter-option">4 Passenger</option>
              </select>
            </div>
          </div>
          <button class="search-btn" type="submit">search</button>
        </form>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  props: {},
  data() {
    return {
      form: {
      city: "",
      days: "",
      budget: ""
      },
      cities: [],
      fetching: false,
    };
  },
  created() {
      const {query} = this.$route;
      console.log(query);
      if (query.city) {
          this.city = query.city
      }
      if (query.days) {
          this.days = query.days
      }
      if (query.budget) {
          this.budget = query.budget
      }
  },
    created() {
    this.fetchCities();
  },
  watch: {
    'form': {
      handler() {
        this.submited()
      },
    deep: true
    }
  },
  methods: {
      submited() {
        this.$router.push({name: 'results', query: this.form})
          
      },
      fetchCities() {
      this.fetching = true;
      fetch(`https://1stquest.com/api/plan/v1/cities`)
        .then(res => res.json())
        .then(res => {
          this.cities = res.data
        })
        .catch(() => {
            this.fetching = false;
            alert("Error in get cities ");
        });
    },
  }
};
</script>

<style>
.filters {
  position: relative;
  padding: 1rem 0 0;
  border-top: 2px solid rgb(230, 229, 229);
  border-bottom: 2px solid rgb(230, 229, 229);
}
.filter-section {
  margin: 0 auto;
  width: 95%;
}
.filter-form {
  display: flex;
  flex-direction: column;
}
.filter {
  width: 100%;
  margin: 0 auto 1rem;
}
.filter-select {
  width: 100%;
  padding: 8px;
  outline: none;
  border-radius: 5px;
  border: 1px solid rgb(240, 239, 239);
  font-size: 16px;
  cursor: pointer;
  appearance: none;
  /* &:active {
        outline: none;
    } */
}
.filter-option {
  font-size: 16px;
  cursor: pointer;
}
.filter-label {
  display: block;
  color: gray;
  padding: 0 0 5px;
  text-transform: capitalize;
}
.search-link {
  text-decoration: none;
  text-transform: capitalize;
  box-shadow: none;
}
.search-btn {
  display: block;
  width: 100%;
  margin: 0 auto 1rem auto;
  text-transform: capitalize;
  padding: 8px;
  border-radius: 5px;
  font-size: 16px;
  background-color: orangered;
  border: none;
  outline: none !important;
  box-shadow: none;
  color: #fff;
  cursor: pointer;
}
.pair-select {
  width: 100%;
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-column-gap: 1rem;
  margin: 0 auto;
}
.home-header-about {
  display: none;
}

@media screen and (min-width: 992px) {
  .filter-section {
    margin: 0 auto 0 2rem;
    width: 920px;
  }
  .filter-form {
    display: flex;
    flex-direction: row;
    align-items: flex-start;
    justify-content: flex-start;
  }
  .filter {
    margin-right: 10px;
    width: 100%;
  }
  .searchbox {
    width: 100%;
  }
  .filter-select {
    width: 100%;
  }
  .filter-label {
    display: none;
  }
  .pair-select {
    width: 160%;
  }
  .search-btn {
    width: 100%;
    margin: 0 auto 0 1rem;
    padding: 10px;
  }
  .home-header-about {
    display: block;
  }
}
select:required:invalid {
  color: gray;
}
option[value=""][disabled] {
  display: none;
}
option {
  color: black;
}
</style>