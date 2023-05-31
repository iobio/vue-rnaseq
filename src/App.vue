<template>
  <div id="vue-splice-junctions-app">
    <splice-junctions
      heading="Splice junctions" 
      locus="chr15:92835700-93031800"
      :tracks="tracksSpliceJunctions"
      genomeBuild="hg38"/>
  </div>
   
</template>

<script>

import SpliceJunctions from './components/SpliceJunctions.vue'

export default {
  name: 'vue-splice-junctions-app',
  components: {
    SpliceJunctions
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
                //url: `https://s3.amazonaws.com/tony.splicejunction.bed/Neural_precursors_SRS011902__exons-novel.sorted.bed.gz`,
                //indexURL: `https://s3.amazonaws.com/tony.splicejunction.bed/Neural_precursors_SRS011902__exons-novel.sorted.bed.gz.tbi`,
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
</style>
