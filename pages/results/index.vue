<template>
  <div class="results">
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
      this.filtering()
    }
  },
  methods: {
    fetchList() {
        this.fetching = true;
      fetch(`https://1stquest.com/api/plan/v1/itineraries`)
        .then(res => res.json())
        .then(res => {
          this.tours = res.data
          this.filtering();
          this.fetching = false;
        })
        .catch(() => {
            this.fetching = false;
            alert("Error in get tours ");
        });
    },
    filtering() {
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
        // tight budget
        if(params.budget && params.budget === 'all') {
            filteredTour = filteredTour.filter(tour => tour.totalPrice.min >= 0  )
        }  
        // tight budget
        if(params.budget && params.budget === '1') {
            filteredTour = filteredTour.filter(tour => tour.totalPrice.min >= 0 && tour.totalPrice.max <= 800 )
        }  
        // mid budget
        if(params.budget && params.budget === '2') {
            filteredTour = filteredTour.filter(tour => tour.totalPrice.min >= 800 && tour.totalPrice.max <= 1000  )
        }   
        // luxury budget
        if(params.budget && params.budget === '3') {
            filteredTour = filteredTour.filter(tour => tour.totalPrice.min >= 1000  )
        } 
      // act query params on data
      return filteredTour;
    }
  }
}
</script>

<style>
</style>