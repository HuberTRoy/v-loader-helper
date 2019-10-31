<template>
  <div>
    <v-loader-style v-if="isLoading" :key="'v-loading'"></v-loader-style>
    <slot v-else></slot>
  </div>
</template>

<script>
export default {
  props: {
    source: {
      require: true
    },
    urls: {
      type: Array,
      default: () => new Array()
    }
  },
  data: function() {
    return {
      isLoading: true,
      _urls: () => new Array()
    }
  },
  methods: {
    translate: function(url) {
      // Remove query.
      url = url.split("?")[0]
      // Remove domain.
      if (url.indexOf("http://") !== -1 || url.indexOf("https://") !== -1) {
        url = url
          .split("/")
          .slice(3)
          .join("/")
      }

      if (!url) {
        return "/"
      }

      if (url[0] !== "/") {
        return `/${url}`
      }

      return url
    }
  },
  watch: {
    source: function() {
      // If data were not empty then change isLoading to false.
      if (this.source) {
        this.isLoading = false
      }
    }
  },
  mounted: function() {
    // Register callback if set moniting urls. 
    if (this.urls) {
      this._urls = this.urls.map(this.translate)
      this.__loader_checks.push((key, value) => {
        if (this._urls.indexOf(key) !== -1) {
          this.isLoading = true
        }
      })
    }
  }
}
</script>
