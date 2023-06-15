<template>
  <v-container>
    <div class="d-flex flex-column">
      <div id="igv-heading" class="d-flex flex-row justify-space-between align-center mb-1" >
          <div id="igv-title">
            {{heading}}
          </div>
          <div class="d-flex flex-row justify-space-between">
            <v-btn flat @click='zoomOut'>
              <v-icon class="igv-zoom-icon" size="22" icon="fa:fas fa-search-minus"></v-icon>
            </v-btn>
            <v-btn flat @click='zoomIn'>
              <v-icon class="igv-zoom-icon"  size="22" icon="fa:fas fa-search-plus"></v-icon>
            </v-btn>
          </div>
          <div>
            <v-btn id="igv-launch-button" @click='launchFullIGV'>
              <v-icon class="igv-zoom-icon" size="16" icon="fa:fas fa-external-link mr-1"></v-icon>
              Full screen
          </v-btn>
          </div>
      </div>
      <div>
        <div id='igv-content'></div>
      </div>
    </div>
  </v-container>
</template>

<script>

import igv from 'igv'

export default {
  name: 'splice-junctions',
  props: {
    heading: String,
    referenceURL: String,
    genomeBuild: String,
    locus: String,
    visible: {
      type: Boolean,
      default: true,
    },
    showLabels: {
      type: Boolean,
      default: false,
    },
    tracks: null
  },
  data () {
    return {
      browser: null,
    }
  },
  mounted: function () {
    if (this.visible) {
      this.init();
    }
  },
  methods: {
    init: function() {
      let self = this;
      const igvDiv = this.$el.querySelector('#igv-content');

      var options = {
        locus: 'chr15:92835700-93031800',
        genome: 'hg38',
        loadDefaultGenomes: true,
        tracks: self.tracks,
      };


      igv.createBrowser(igvDiv, options).then((browser) => {
        this.browser = browser;
      })
    },
    zoomOut: function() {
      this.browser.zoomOut();
    },
    zoomIn: function() {
      this.browser.zoomIn();
    },
    launchFullIGV: function() {
      launchIGV(this.referenceURL, this.locus, this.tracks);
    },
  },
  watch: {
    visible: function() {
      if (!this.browser) {
        this.init();
      }
      else if (!this.visible) {
        igv.removeBrowser(this.browser);
        this.browser = null;
      }
      //igv.visibilityChange();
    },
  }
}

function launchIGV(referenceURL, locus, tracks) {

  var options = {
    loadDefaultGenomes: true,
    locus: 'chr15:92835700-93031800',
    genome: 'hg38',
    tracks: tracks,
  };

  

  const url = 'https://s3.amazonaws.com/static.iobio.io/dev/igv.iobio.io/index.html?config=' + JSON.stringify(options)
  window.open(url, '_blank')
}

</script>

<style>

#igv-heading {
  color: #616161;
}
#igv-title {
  font-size: 18px;
  font-weight: 600;
}
.igv-zoom-icon {
  color: #616161;
}
#igv-launch-button {
  font-weight: 600;
}

.igv-right-hand-gutter {
  right: initial;
  left: -10px;
}

.igv-content-header {
  //display: none;
}

</style>