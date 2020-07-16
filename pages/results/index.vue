<template>
  <div class="results">
    <!-- <Header /> -->
    <!-- <Filters /> -->
    <h3 v-if="fetching">Fetching ...</h3>
    <ToursList v-else :tours="filteredTours"  />
  </div>
</template>

<script>
import ToursList from "@/components/tour/list";

export default {
  data() {
    return {
      tours: [],
      fetching: false,
      filteredTours: []
    };
  },
  components: {
    ToursList
  },
  created() {
    this.fetchList();
  },
  watch:{
    "$route.query": function(){
      console.log("params change", this.$route);
      this.startFilter()
    }
  },
  methods: {
    fetchList() {
        this.fetching = true;
      fetch(`https://1stquest.com/api/plan/v1/itineraries`)
        .then(res => res.json())
        .then(res => {
          this.tours = res.data
          this.startFilter();
          this.fetching = false;
        })
        .catch(() => {
            this.fetching = false;
            alert("Error in get tours ");
        });
    },
    startFilter() {
      const { query } = this.$route;

      this.filteredTours = this.doFilter(this.tours, query);
    },
    doFilter(list, params) {
      let filteredTour = list
      if(params.city  && params.city !== 'All') {
            filteredTour = list.filter(tour => {
                    for(let cityIndex = 0; cityIndex < tour.cities.length ; cityIndex++) {
                        let city = tour.cities[cityIndex]
                          if(city.name && city.name === params.city ) {
                                return tour
                            }
                    }
            })
      }
        if(params.days && params.days !== 'all' ) {
            filteredTour = filteredTour.filter(tour => {
                if(tour.cities) {
                    for(let cityIndex = 0; cityIndex < tour.cities.length ; cityIndex++) {
                        let city = tour.cities[cityIndex]
                        if(city.days && city.days.toString() === params.days ) {
                            return tour
                        }
                    }
                }
            })
        }
      // act query params on data
      return filteredTour;
    }
  }
}
</script>

<style>
</style>