<template>
  <div class="page-wrapper full-screen">
    <div style="height:100vh;width:100vw;">
      <!-- PANEL -->
      <div class="panel">
        <h1 style="padding-left:30px; padding-top:30px;">Lit Events Tonight</h1>
        <!-- EVENTS GRID -->
        <div class="gutter-example">
          <a-row :gutter="16">
            <a-col class="gutter-row" :xs="{span: 24}" :sm="{span: 24}" :md="{span: 12}" :lg="{span: 12}">
              <!-- A CARD -->
              <a>
                <a-card class="event-card">
                  <img
                    alt="example"
                    src="https://d3nxoulyw7bc8u.cloudfront.net/images/events/5a1f11cd-9bb2-44ef-a60a-c47fb8cb7733.jpg"
                    slot="cover"
                  />
                  <a-card-meta title="Official Lexani Afterparty 2019 with DJ Quik">
                    <template slot="title">Chateau</template>
                    <template slot="description">10:30 PM - 11:55 PM</template>
                  </a-card-meta>
                  <!-- <template class="ant-card-actions" slot="actions">
                    <a-icon type="schedule" />
                    <a-icon type="calendar" />
                  </template> -->
                </a-card>
              </a>
            </a-col>
            <a-col class="gutter-row" :xs="{span: 24}" :sm="{span: 24}" :md="{span: 12}" :lg="{span: 12}">
              <!-- ANOTHER CARD -->
              <a>
                <a-card class="event-card">
                  <img
                    alt="example"
                    src="https://d3nxoulyw7bc8u.cloudfront.net/images/events/d6f69d69-3e3c-48b7-941f-f5e6081f14b8.jpg"
                    slot="cover"
                  />
                  <a-card-meta title="DJ Zo Sound / Color Industry Wednesdays">
                    <template slot="title">On The Record</template>
                    <template slot="description">10:30 PM - 4:00 AM</template>
                  </a-card-meta>
                </a-card>
              </a>
            </a-col>
            <a-col class="gutter-row" :xs="{span: 24}" :sm="{span: 24}" :md="{span: 12}" :lg="{span: 12}">
              <!-- A CARD -->
              <a>
                <a-card class="event-card">
                  <img
                    alt="example"
                    src="https://d3nxoulyw7bc8u.cloudfront.net/images/events/5a1f11cd-9bb2-44ef-a60a-c47fb8cb7733.jpg"
                    slot="cover"
                  />
                  <a-card-meta title="Official Lexani Afterparty 2019 with DJ Quik">
                    <template slot="title">Chateau</template>
                    <template slot="description">10:30 PM - 11:55 PM</template>
                  </a-card-meta>
                </a-card>
              </a>
            </a-col>
            <a-col class="gutter-row" :xs="{span: 24}" :sm="{span: 24}" :md="{span: 12}" :lg="{span: 12}">
              <!-- A CARD -->
              <a>
                <a-card class="event-card">
                  <img
                    alt="example"
                    src="https://d3nxoulyw7bc8u.cloudfront.net/images/events/5a1f11cd-9bb2-44ef-a60a-c47fb8cb7733.jpg"
                    slot="cover"
                  />
                  <a-card-meta title="Official Lexani Afterparty 2019 with DJ Quik">
                    <template slot="title">Chateau</template>
                    <template slot="description">10:30 PM - 11:55 PM</template>
                  </a-card-meta>
                </a-card>
              </a>
            </a-col>
          </a-row>
        </div>
      </div>
      <!-- MAP PANE -->
      <div class="map-pane">
        <MglMap :accessToken="accessToken" :mapStyle="mapStyle" :center="center" :zoom="10">
          <!-- CONTROLS -->
          <!-- <MglGeolocateControl position="bottom-right" /> -->
          <MglNavigationControl position="top-right" />
          <!-- DRAIS -->
          <MglMarker :coordinates="drais" @click="onMarkerClick">
            <MglPopup anchor="bottom" style="margin:5%;">
              <div class="popup-container">
                <div>
                  <img src="https://d3nxoulyw7bc8u.cloudfront.net/images/venue_template/0ce9dc86-5093-4202-83bb-89bd299fd9a8.jpg" alt="" srcset="" style="height:50%;">
                  <h1>Drais Nightclub</h1>
                  <p>3595 S Las Vegas Blvd</p>
                  <a href="/venue/drais">Visit Club Page</a>
                </div>
              </div>
            </MglPopup>
          </MglMarker>
        </MglMap>
      </div>
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex'
import ProductList from '@/components/ProductList'
import AddProduct from '@/components/AddProduct'
import Mapbox from "mapbox-gl";
import { MglMap, MglMarker, MglPopup, MglGeolocateControl, MglNavigationControl } from "vue-mapbox";

export default {
  components: { ProductList, AddProduct, MglMap, MglPopup, MglMarker, MglGeolocateControl, MglNavigationControl },
  computed: mapState('app', ['networkOnLine']),
  data() {
    return {
      accessToken: "pk.eyJ1Ijoib2Jpbm5hLWl6enpsaXQiLCJhIjoiY2sxNXh5aXJjMDE5MDNobWoxZ29hbXNxYyJ9.N_Go-CocmmlnDfl-cnJGkA", // your access token. Needed if you using Mapbox maps
      mapStyle: "mapbox://styles/obinna-izzzlit/ck15zi1t22xuw1cq6cugyg14f", // your map style
      center: [-115.132921, 36.122325], // Las Vegas Center Coordinates
      coordinates: [-115.132921, 36.122325], // Vegas
      drais: [-115.171790, 36.115020],
    };
  },
  created() {
    // We need to set mapbox-gl library here in order to use it in template
    this.mapbox = Mapbox;
  },
  methods: {
    async onMarkerClick(payload) {
      // get the params from the payload
      let marker = payload.marker
      let markerComponent = payload.component
      let map = payload.map
      
      // get the coordinates
      let markerCoords= markerComponent.coordinates

      // fly the map to the new center
      const newParams = await map.flyTo({
        center: markerCoords,
        zoom: 12,
        speed: 1
      })

      // scrollTo & highlight the correct event in the panel

    }
  }
}
</script>

<style lang="scss" scoped>
@import '@/theme/variables.scss';

.products-page-title {
  text-align: center;
  margin-bottom: 60px;
}

.product-list {
  margin: 20px 0;
}

.panel {
  height: 100vh;
  width:45vw; 
  position: absolute;
  z-index:10;
  overflow: auto;
}

.map-pane {
  height: 100vh;
  width:55vw;
  z-index:10;
  position: absolute;
  right: 0;
}

.gutter-example >>> .ant-row > div {
    background: transparent;
    border: 0;
    padding-left: 16px;
    padding-right: 16px;
  }
  .gutter-example {
    padding-left: 16px;
    padding-right: 16px;
  }

  .gutter-box {
    background: #00a0e9;
    padding: 5px 0;
    margin-bottom: 16px;
  }

  .gutter-row{
    padding-top: 16px;
  }

  .active {
    border: 2px solid $vue-color;
  }

  .event-card {
    margin: 10%;
  }
  
  .popup-container {
    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: auto;
  }
  /* */

  
  /* On screens that are 440px or less, move the panel to bottom */
  @media screen and (max-width: 440px) {
    .panel {
      height: 50vh;
      width: 100vw; 
      position: absolute;
      bottom: 0;
      z-index: 10;
      overflow: auto;
    }

    .map-pane{
      height: 50vh;
      width: 100vw;
      z-index: 10;
      position: absolute;
      top: 0;
     }
  } 

</style>
