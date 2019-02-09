

<template>
<div class="content-apply">
    <div class="apply-addMovie">
        <span>Nouveau film</span><br />
        Titre: <br /><input type="text" v-model="movie_to_add.title" /><br />
        affiche : <br /><input type="text" v-model="movie_to_add.affiche" /><br />
        langue : <br /><input type="text" v-model="movie_to_add.langue" /><br />
        Année : <br /><input type="text" v-model="movie_to_add.year" /><br />
        Synopsys : <br /><textarea v-model="movie_to_add.synopsys"></textarea><br />
        genre : <br/><input v-model="movie_to_add.genre"><br />
        <button v-on:click="newmovie2">Add</button>
    </div>
    <input class="rechercheBar" type="text" v-model="search" placeholder="Search" /><p>Movie number : {{movies.length}}</p>

    <ul>
        <movie-item v-for="(movie, index) in movies_search" v-bind:key="movie.title" v-bind:movie="movie" v-on:edit="edit(movie)" v-on:note="addnote(movie)" v-on:remove="remove(index)"></movie-item>
    </ul>

    <div class="modal-edit" v-if="movie_to_edit">
        Modifier le film<br /><br />
        Titre : <br/><input type="text" v-model="movie_to_edit.title" /><br />
        affiche : <br/><input type="text" v-model="movie_to_edit.affiche" /><br />
        langue : <br /><input type="text" v-model="movie_to_edit.langue" /><br />
        Année : <br/><input type="text" v-model="movie_to_edit.year" /><br />
        Synopsys : <br/><textarea v-model="movie_to_edit.synopsys"></textarea><br />
        genre : <br/><input v-model="movie_to_edit.genre"><br />
        <button v-on:click="save">Save</button>
    </div>

    <p class="modal-edit" v-if="movie_to_notes">
        Note du film<br />
        note :
        <input type="numbre" id="inputnote" name="vote" v-model="movie_to_notes"><br />
        <button v-on:click="savenote">Save</button>
    </p>

</div>
</template>

<script>
export default {
    data() {
        return {
            movie_to_add: {},
            movie_to_edit: null,
            movie_to_notes: null,
            search: "",
            movies : [
                {
                    title: "Blade Runner",
                    affiche: "https://horrornews.net/wp-content/uploads/2015/05/Blade-Runner-poster-4.jpg",
                    langue:"Français",
                    year: 1982,
                    synopsys: "Dans les dernières années du 20ème siècle, des milliers d'hommes et de femmes partent à la conquête de l'espace, fuyant les mégalopoles devenues insalubres. Sur les colonies, une nouvelle race d'esclaves voit le jour : les répliquants, des androïdes que rien ne peut distinguer de l'être humain. ",
                    notes: [3,4,4,5],
                    genre:"science-fiction",
                    Réalisateur:[{Nom:"Ridley Scott",Nationalité:"Anglaise",naissance:"30 novembre 1937"}]
                },
                {
                    title:"Akira",
                    affiche: "http://fr.web.img2.acsta.net/c_215_290/medias/nmedia/18/64/25/05/19199449.jpg",
                    langue:"Japonais",
                    year:2007,
                    synopsys:"Tetsuo, un adolescent ayant vécu une enfance difficile, est la victime d'expériences visant à développer les capacités psychiques qui dorment en chacun de nous. Ainsi doté d'une puissance que lui meme ne peut imaginer, Tetsuo décide de partir en guerre contre le monde qui l'a opprimé. Dès lors, Il se retrouve au coeur d'une légende populaire qui annonce le retour prochain d'Akira, un enfant aux pouvoirs extra-ordinaires censé délivrer Tokyo du chaos... ",
                    notes: [3,1,4,5],
                    genre:"animation",
                    Réalisateur:[{Nom:"Katsuhiro Ōtomo",Nationalité:"Japonaise",naissance:"14 avril 1954 "}]
                },
            ]
        }
    },

    methods: {
        newmovie1: function() {
            this.movies.push({title:"New movie"})
        },
        newmovie2: function() {
            this.movies.push(this.movie_to_add)
            this.movie_to_add = {}
        },

        edit: function(movie) {
            this.movie_to_edit = movie
        },
        save: function() {
            this.movie_to_edit = null
        },
        remove: function(index) {
            this.movies.splice(index, 1)
        },
        addnote: function(movie){
          this.movie_to_notes = movie.notes
        },
        savenote: function(movie){
          this.movie_to_notes = null
        }
    },

    created: function() {
        console.log("Created")
    },

    computed: {
        firstletter: function() {
            return this.message[0]
        },
        movies_search: function() {
            return this.movies.filter(m => m.title.toLowerCase().indexOf(this.search.toLowerCase())!=-1);
        }
    }
}
</script>
