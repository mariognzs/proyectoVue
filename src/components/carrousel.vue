<script>
export default {
  data() {
    return {
      obj: {
        imagenes: [
          "https://www.supercars.net/blog/wp-content/uploads/2020/09/2020-Lamborghini-Aventador-SVJ-Roadster-Xago-Edition-001-2160-scaled.jpg",
          "https://www.supercars.net/blog/wp-content/uploads/2020/12/2021-Lamborghini-Huracan-STO-005-2160-scaled.jpg",
          "https://images.alphacoders.com/887/thumb-1920-887950.jpg",
          "https://wallpaperaccess.com/full/409240.jpg",
          "https://i.pinimg.com/originals/32/0a/a8/320aa8b314e8397a69ce5ca791b0707f.jpg",
        ],
        cars: ["AVENTADOR", "HURACÁN", "URUS", "GALLARDO", "MURCIELAGO"],
      },
    };
  },
};
</script>

<template>
  <div class="ms-5">
    <div class="m-1">
      <div class="container-fluid ms-5 mt-5">
        <v-carousel
          cycle
          height="400"
          hide-delimiter-background
          show-arrows="hover"
        >
          <v-carousel-item
            width="100%"
            v-for="(car, i) in obj.cars"
            :key="i"
            :src="obj.imagenes[i]"
            cover
          >
            <div class="d-flex fill-height justify-center align-center">
              <div class="text-h2 text-white">Lamborghini {{ car }}</div>
            </div>
          </v-carousel-item>
        </v-carousel>
      </div>
    </div>
  </div>
</template>
