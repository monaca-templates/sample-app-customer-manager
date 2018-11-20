<template>
  <div id="mapbox"></div>
</template>

<script>
  import mapboxgl from 'mapbox-gl'
  import MapboxLanguage from '@mapbox/mapbox-gl-language'
  import geocoding from '@mapbox/mapbox-sdk/services/geocoding'
  import { MAPBOX_API_TOKEN } from '../../consts/consts.js'

  export default {
    name: 'Map',
    props: {
      address: {
        type: String,
        default: '',
      }
    },
    data: () => {
      return {
        center: [139.7521, 35.6825], // デフォルトは皇居
        map: {},
        geocodingClient: {},
        language: 'ja'
      }
    },
    computed: {
      adjustedQuery () {
        // APIの仕様で20文字以下でのみ検索可能
        return this.address.substr(0, 19)
      }
    },
    methods: {
      initGeocodingClient () {
        // 緯度経度検索API
        this.geocodingClient = geocoding({
          accessToken: MAPBOX_API_TOKEN
        })
      },
      searchCoordinates () {
        // 所在地から緯度経度を検索
        this.geocodingClient.forwardGeocode({
          query: this.adjustedQuery,
        })
        .send()
        .then((res) => {
          let coordinates = res.body.features[0]
          // 結果が得られた場合はその緯度経度を中心としてマップを表示
          this.center = coordinates ? coordinates.center : this.center
          this.renderMap()
        })
      },
      renderMap () {
        mapboxgl.accessToken = MAPBOX_API_TOKEN
        // マーカー（ピン）のオブジェクト
        this.map = new mapboxgl.Map({
          container: 'mapbox',
          center: this.center,
          zoom: 13,
          style: 'mapbox://styles/mapbox/streets-v9'
        })
        const language = new MapboxLanguage()
        this.map.addControl(language)
        this.renderMarker()
        this.map.on('load', () => {
          this.setMapLanguage()
        })
      },
      renderMarker () {
        const marker = new mapboxgl.Marker()
          .setLngLat(this.center)
          .addTo(this.map)
      },
      setMapLanguage () {
        this.map.setLayoutProperty('country-label-lg', 'text-field', ['get', 'name_' + this.language])
      }
    },
    mounted () {
      this.initGeocodingClient()
      if (this.adjustedQuery) {
        this.searchCoordinates()
      } else {
        // 所在地が入力されていなければデフォルト地点を表示
        this.renderMap()
      }
    }
  }
</script>
