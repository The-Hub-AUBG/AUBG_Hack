<template>
  <GmapMap
    ref="mapRef"
    :center="{ lat: 10, lng: 10 }"
    :zoom="7"
    map-type-id="terrain"
    style="width: 1000px; height: 700px"
  >
    <GmapMarker
      :key="index"
      v-for="(m, index) in markers"
      :position="m.position"
      :clickable="true"
      :draggable="true"
      :icon="markerColor(m.free)"
      @click="center = m.position"
    />
  </GmapMap>
</template>

<script>
export default {
  data() {
    return {
      markers: [
        {
          position: {
            lat: 1.38,
            lng: 103.8
          },
          free: true,
        },
        {
          position: {
            lat: 53.168057,
            lng: 8.654234
          },
          free: true,
        },
        {
          position: {
            lat: 42.659372,
            lng: 23.314266
          },
          free: false,
        }
      ]
    };
  },
  methods: {
    markerColor(isFree) {
      if(isFree) {
        return 'http://maps.google.com/mapfiles/ms/icons/green-dot.png'
      } else {
        return 'http://maps.google.com/mapfiles/ms/icons/red-dot.png'
      }
    }
  },
  mounted() {
    this.$refs.mapRef.$mapPromise.then(map => {
      map.panTo({ lat: 1.38, lng: 103.8 });
    });
  }
};
</script>
