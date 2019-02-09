<template>
  <div class="film">
            <div class="film-img">
              <img v-bind:src="movie.affiche" />
            </div>
            <div class="film-text">
              <h3>{{ movie.title }} ({{ movie.year }})</h3>
                  {{moyenne}}/5
              <button class="button-vote" v-on:click="addnote">voter</button>
              <p> {{ movie.synopsys }}</p>
              <p> {{ movie.langue}}</p>
              <p>{{ movie.genre }} </p>
               <button class="button-remove" v-on:click="remove">Remove</button><button class="button-edit" v-on:click="edit">Edit</button></p>
            </div>
    </div>
</template>
<script>
export default{
    data(){
        return{
        }
    },
    props:['movie'],
    methods:{
        remove:function(){
          this.$emit('remove',this.index);
        },
        edit:function(){
            this.$emit('edit',this.movie);
        },
        addnote:function(){
            this.$emit('note',this.movie);
        }
    },
    computed: {
      moyenne: function(){
        let not = this.movie.notes;
        let moy = 0;
        not.forEach(function(element) {
          moy = moy + element;
        });
        moy = moy /not.length;
        return moy.toFixed(1);
      }
    }
}
</script>
