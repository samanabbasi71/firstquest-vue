<template>
  <div>
    <div v-if="fetching">Fetching tour</div>
    <div v-else>
      <div class="tourpage__container">
        <header class="header">
          <h3 class="header-slug">iran trip planer</h3>
          <div class="header-info">
            <div class="breadcrumb">
              <nuxt-link to="/" class="breadcrumb-link">
                <p class="breadcrumb-item">1stQuest</p>
              </nuxt-link>
              <p class="breadcrumb-item breadcrumb-p">/</p>
              <p class="breadcrumb-item">{{tour.slug}}</p>
            </div>
            <h1 class="header-title">{{tour.title}}</h1>
            <p class="header-about">{{tour.overView}}</p>
            <a href="#story" class="header-anchor">read story of this on</a>
          </div>
        </header>
        <div class="tour-content">
          <section class="tour-section" id="visa">
            <p class="tour-section-title">get iran e-visa and travel insurance</p>
            <p
              class="tour-section-info"
            >Lorem ipsum dolor sit amet consectetur adipisicing elit. Eum deleniti nemo iste provident fuga delectus tempora eius voluptates recusandae ut ea corporis commodi iure, quibusdam exercitationem animi iusto, alias quasi perferendis accusamus labore inventore voluptas eveniet facilis. Nemo numquam officia itaque. Debitis placeat ipsum consequatur ut odit maiores veritatis praesentium?</p>
            <div class="tour-cards">
              <nuxt-link to="#" class="tour-card">
                <div class="tour-card-top">
                  <p class="tour-section-title">
                    <span class="tour-card-icon">
                      <i class="fa fa-book"></i>
                    </span> iran online visa aplication form
                  </p>
                </div>
                <p class="tour-card-bottom">
                  between $
                  <span>19</span> - $
                  <span>29</span>
                </p>
              </nuxt-link>
              <nuxt-link to="#" class="tour-card">
                <div class="tour-card-top">
                  <p class="tour-section-title">
                    <span class="tour-card-icon">
                      <i class="fa fa-shield"></i>
                    </span> iran travel insurance
                  </p>
                </div>
                <p class="tour-card-bottom">
                  between $
                  <span>19</span> - $
                  <span>29</span>
                </p>
              </nuxt-link>
            </div>
          </section>
        </div>
        <div class="tour-content" v-for="(city, index) in tour.cities" :key="index">
          <section class="tour-section" id="visa">
            <p class="tour-section-title">{{city.name}}</p>
            <p>{{city.days}} Days</p>
            <p class="tour-section-info">{{city.thingsToDo}}</p>
            <div class="tourpage-images">
              <img v-for="(image, index) in city.images" :key="index" :src="image.src" class="tourpage-img" />
            </div>
            <p class="tour-section-info">cost and services in {{city.name}}</p>
            <div class="tour-cards">
              <nuxt-link to="#" class="tour-card">
                <div class="tour-card-top">
                  <p class="tour-section-title">
                    <span class="tour-card-icon">
                      <i class="fa fa-car"></i>
                    </span> pick-up
                  </p>
                </div>
                <p>From Airport To Hotel</p>
                <p class="tour-card-bottom">$ 19</p>
              </nuxt-link>
              <nuxt-link to="#" class="tour-card">
                <div class="tour-card-top">
                  <p class="tour-section-title">
                    <span class="tour-card-icon">
                      <i class="fa fa-building"></i>
                    </span> Hotel
                  </p>
                </div>
                <p>Grand Hotel {{city.name}}</p>
                <p class="tour-card-bottom">
                  between $
                  <span>19</span> - $
                  <span>29</span>
                </p>
              </nuxt-link>
            </div>
          </section>
        </div>
      </div>
    </div>
  </div>
  <!--  -->
</template>

<script>
export default {
  layout: 'singlepage',
  data() {
    return {
      tour: {},
      fetching: false
    };
  },
  created() {
    console.log("detail created", this.$route.params);
    const { slug } = this.$route.params;
    this.fetchTour(slug);
  },
  methods: {
    fetchTour(slug) {
      this.fetching = true;
      fetch(`https://1stquest.com/api/plan/v1/itinerary/${slug}`)
        .then(res => res.json())
        .then(res => {
          this.tour = res.data;
          this.fetching = false;
        })
        .catch(() => {
          this.fetching = false;
          alert("Error in fetching");
        });
    }
  }
    // data() {
    //   return {
    //     tour: {}
    //   };
    // }

    //   async fetch() {
    //     this.tour = await fetch(`https://1stquest.com/api/plan/v1/itinerary/${this.$route.params.id}`).then((res) => res.json()).then((res) => res.data)
    //     console.log(tour);
    //   }
};
</script>

<style scoped>
.main-header {
  min-height: calc(30vh);
  /* background: linear-gradient(rgba(0,0,0,0.05), rgba(0,0,0,0.05)); */
  background-image: url("~@/assets/img/1.png");
  background-position: center;
  background-size: cover;
  background-repeat: no-repeat;
  transition: all 0.3s ease-in-out;
  color: #fff;
  text-transform: capitalize;
  padding: 1.5rem 1.5rem 4rem;
  font-size: 1.3rem;
  line-height: 35px;
}

@media screen and (min-width: 768px) {
  .main-header {
    min-height: calc(50vh);
  }
}

.header {
  min-height: calc(120vh);
  /* background: linear-gradient(rgba(0,0,0,0.3), rgba(0,0,0,0.3)); */
  background-image: url("~@/assets/img/1.png");
  background-position: center;
  background-size: cover;
  background-repeat: no-repeat;
  transition: all 0.3s ease-in-out;
  color: #fff;
  text-transform: capitalize;
  padding: 1.5rem 1.5rem 4rem;
  font-size: 1.3rem;
  line-height: 35px;
}
@media screen and (min-width: 552px) {
  .header {
    min-height: calc(100vh);
  }
}
@media screen and (min-width: 768px) {
  .header {
    min-height: calc(80vh);
  }
}
@media screen and (min-width: 992px) {
  .header {
    min-height: calc(60vh);
  }
}
.breadcrumb {
  display: flex;
}
.breadcrumb-p {
  padding: 0 10px;
}
.breadcrumb-link {
  text-decoration: none;
  color: blue;
  transition: all 0.3s ease;
  /* &:hover {
        text-decoration: none;
        color: #fff;
    } */
}
.header-title {
  margin: 0.8rem 0;
  line-height: 50px;
  padding: 0 1rem;
  text-transform: uppercase;
}
.header-about {
  text-align: justify;
  text-justify: inter-word;
}
.header-anchor {
  color: #fff;
  /* &:focus {
        color: #fff;
    } */
}
.tour-content {
  padding: 2rem;
}
.tour-section {
}
.tour-section-title {
  color: black;
  font-weight: bolder;
  font-size: 20px;
  text-transform: capitalize;
}
.tour-section-info {
  margin: 1rem 0 2rem;
  text-transform: capitalize;
}
.tour-cards {
  display: flex;
  flex-direction: column;
}
.tour-card {
  text-decoration: none;
  color: black;
  background-color: #fff;
  box-shadow: 3px 2px 3px 2px (rgba(119, 119, 119, 0.3));
  border: 1px solid grey;
  border-radius: 10px;
  padding: 1rem;
  margin: 0 1rem 1rem 0;
  /* &:focus {
        color: black;
    } */
}
.tour-card-bottom {
  color: red;
  /* span {
        font-weight: bolder;
        font-size: 20px;
        padding: 5px 0;
    } */
}
@media screen and (min-width: 768px) {
  .tour-cards {
    display: flex;
    flex-direction: row;
  }
  .tour-card {
    flex: 1 1 49%;
  }
}
.tourpage-images {
}
.tourpage-img {
  border-radius: 5px;
  margin: 0 1rem 1rem 0;
}
.tourpage-images-link {
  margin-bottom: 1rem;
}
</style>