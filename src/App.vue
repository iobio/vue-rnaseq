<template>
  <div id="vue-splice-junctions-app">
    <RNASeqIGV
      heading="Splice junctions" 
      locus="chr15:92835700-93031800"
      :tracks="tracksSpliceJunctions"
      genomeBuild="hg38"/>
  </div>
   
</template>

<script>

import RNASeqIGV from './components/RNASeqIGV.vue'

export default {
  name: 'vue-splice-junctions-app',
  components: {
    RNASeqIGV
  },
  data()  {
    let self = this;
    return {
      tracksSpliceJunctions:  [
        {
          type: 'merged',
          name: 'Splice Junctions',
          height: 200,
          tracks: [
            {
                type: 'junction',
                name: 'Junctions',
                format: 'bed',
                url: `https://www.dropbox.com/s/nvmy55hhe24plpv/splice_junction_track_test_cases_sampleA.chr15-92835700-93031800.SJ.out.bed.gz?dl=0`,
                indexURL: `https://www.dropbox.com/s/iv5tcg3t8v3xu23/splice_junction_track_test_cases_sampleA.chr15-92835700-93031800.SJ.out.bed.gz.tbi?dl=0`,
                displayMode: 'COLLAPSED',
                minUniquelyMappedReads: 1,
                minTotalReads: 1,
                maxFractionMultiMappedReads: 1,
                minSplicedAlignmentOverhang: 0,
                thicknessBasedOn: 'numUniqueReads', //options: numUniqueReads (default), numReads, isAnnotatedJunction
                bounceHeightBasedOn: 'random', //options: random (default), distance, thickness
                colorBy: 'isAnnotatedJunction', //options: numUniqueReads (default), numReads, isAnnotatedJunction, strand, motif
                labelUniqueReadCount: true,
                labelMultiMappedReadCount: true,
                labelTotalReadCount: false,
                labelMotif: false,
                labelIsAnnotatedJunction: " [A]",
                hideAnnotatedJunctions: false,
                hideUnannotatedJunctions: false,
                hideMotifs: ['GT/AT', 'non-canonical'], //options: 'GT/AG', 'CT/AC', 'GC/AG', 'CT/GC', 'AT/AC', 'GT/AT', 'non-canonical'
            },
            {
                type: 'wig',
                name: 'Coverage',
                format: "bigwig",
                url: 'https://www.dropbox.com/s/8j2uf0hsqprusnc/splice_junction_track_test_cases_sampleA.chr15-92835700-93031800.bigWig?dl=0',
            }
          ]          
        } 
      ]  
    }
  }
}
</script>

<style>
#vue-splice-junctions-app {
  width: 100%;
}

.application, .v-application, body {
  font-family: 'Poppins' !important;
  font-size: 15px;
}


.v-app-bar {
  font-size:  16px;
}
.v-app-bar .v-btn {
  font-size: 16px;
}

.v-btn.v-size--default {
    font-size: 15px;
}
.v-btn {
    letter-spacing: initial;
    text-transform: initial;
}
.v-chip.v-size--default {
  height: 24px;
  font-size: 13px;
  padding: 5px ;
  border-radius: 5px;
}
h1, .h1 {
    font-size: 20px !important;
    margin-top: 0px !important;
    margin-bottom: 5px !important;
}
h2, .h2 {
    font-size: 18px !important;
    margin-top: 0px !important;
    margin-bottom: 5px !important;
}
.v-card {
  padding: 10px !important;
}
.v-card.full-width-card {
  margin-left:   10px !important;
  margin-right:  10px !important;
  margin-top:    5px !important;
  margin-bottom: 5px !important;
  width: 100% !important
}

</style>