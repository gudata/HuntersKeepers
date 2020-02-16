<template>
  <div>
    <ul>
      <li v-for="move in moves"><input type="checkbox" :checked="move.has_move"><strong>{{move.name}}:</strong> {{move.description}}</li>
    </ul>
    <b-button @click="submitMoves">Submit Moves</b-button>
  </div>
</template>

<script>
export default {
  computed: {
    selectedMoves: function() {
      return this.moves.filter((move) => {
        console.log(move.has_move);
        return move.has_move;
      });
    }
  },
  data: function () {
    return {
      moves: []
    }
  },
  methods: {
    submitMoves() {
      put('/hunters/${hunter_id}', { 'moves_attributes': this.selectedMoves });
    }
  },
  mounted: function() {
    fetch(`/moves.json?hunter_id=${this.hunter_id}`)
      .then(response => response.json())
      .then((moves) => this.moves = moves);
  },
  props: ['hunter_id'],
}
</script>
