<template>
  <v-container>
    <v-card>
      <v-layout column>
        <v-layout row justify-space-between>
          <v-flex xs3>
            {{heading}}
          </v-flex>
          <v-layout xs3 justify-center>
            <v-btn fab small @click='zoomOut'>
              <v-icon>zoom_out</v-icon>
            </v-btn>
            <v-btn fab small @click='zoomIn'>
              <v-icon>zoom_in</v-icon>
            </v-btn>
          </v-layout>
          <v-flex xs3>
            <v-btn @click='launchFullIGV'>Open IGV in a Tab</v-btn>
          </v-flex>
        </v-layout>
        <v-flex xs12>
          <div id='igv-content'></div>
        </v-flex>
      </v-layout>
    </v-card>
  </v-container>
</template>

<script>

import igv from '../../lib/igv.esm'

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

.igv-right-hand-gutter {
  right: initial;
  left: -10px;
}

.igv-content-header {
  //display: none;
}

</style>
