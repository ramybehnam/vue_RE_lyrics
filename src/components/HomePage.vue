<template>
<!-- container for the hole page -->
<div id="container">
    <!-- conains the header of the page -->
    <div id="header">
        <h1>RE-Lyrics</h1>
    </div>
    <!-- contains all element for the serach function  -->
    <div id="search_area">
        <h2>Search lyrics for you favorit songs </h2>
        <br>
        <form @submit.prevent="submitted">
            <input type="text" v-model="songName" id="songName" placeholder="Song Name" class="sInput">
            <br>
            <input type="text" v-model="artistName" id="songName" placeholder="Artist Name" class="sInput">
            <br>
            <button type="button" id="btnSearch" @click="searchFunction()">Search</button>
        </form>
        <br>
        <button v-on:click="showListView = !showListView" type="button" id="btnMyList" @click="myListFunction()">My list</button>
        <br>

        <div v-show="!showListView" id="myListView">
            <h2>Search for your saves lyrics</h2>
            <br>
            <input v-model="mySongName" type="text" id="myListInput" placeholder="Enter you saved song name here">
            <br>
            <button type="button" id="btnShowMySavedSong" @click="showMyLyrics()">Show lyrics</button>
            <h5 id="myLyrics"> {{mySavedLyrics}}</h5>
        </div>
    </div>
    <!-- continer the elemnt to show and save lyrics -->
    <div v-if="lyrics" id="lyrics_area">
        <h5> {{lyrics}}</h5>
        <br>
        <button type="button" id="btnSaveToMyList" @click="saveToMyList()">Save to my list</button>
        <br>
    </div>
</div>
</template>

<script>
import axios from "axios";
export default {

    data() {
        return {
            songName: "",
            artistName: "",
            lyrics: "",
            mySavedLyrics: "",
            showListView: true,
            mySongName: "",
        };
    },

    // contins all methods
    methods: {

        // function for the search button
        searchFunction() {
            axios.get('https://api.lyrics.ovh/v1/'+ this.artistName + '/' + this.songName)
                .then(res => this.lyrics =res.data.lyrics);
                this.showListView = true;

        },

        // function for saving lyrics to localstorage
        saveToMyList() {
            localStorage.setItem(this.songName, this.lyrics);
            alert( this.songName +" is know added to your song list!")
        },

        // function for retrieving the saves song lyrics
        showMyLyrics() {
            this.lyrics = null;
            this.mySavedLyrics = localStorage.getItem(this.mySongName);
        },

        // function to manage the showing of the different lyrics elements
        myListFunction() {
            this.lyrics = null;
            this.mySavedLyrics = null;
            this.mySongName = null;
        },

    },
};
</script>

<style>
/* style for the header */
h1 {
    padding: 40px 0px;
    font-size: 80px;
}

/* style for evrithing within the search area  */
#search_area {
    background-color: rgb(29, 42, 52);
    padding-top: 60px;
    padding-bottom: 60px;
}

.sInput {
    background-color: rgb(42, 62, 82);
    width: 800px;
    height: 50px;
    margin-bottom: 10px;
    color: rgb(252, 118, 162);
    font-size: 16px;
    padding-left: 15px;

}

#btnSearch {
    background-color: rgb(66, 185, 132);
    width: 500px;
    height: 40px;
    border: none;
    font-size: 16px;
    font-weight: bold;
    color: rgb(42, 62, 82);
    margin-top: 30px;
}

#btnMyList {
    background-color: rgb(252, 118, 162);
    width: 500px;
    height: 40px;
    border: none;
    font-size: 16px;
    font-weight: bold;
    color: rgb(42, 62, 82);
    margin-top: 30px;
    margin-bottom: 50px;
}

::placeholder {
    color: rgb(66, 185, 132);
}

#myListView {
    border: solid 2px rgb(252, 118, 162);
    width: 1000px;
    margin: 0 auto;
    padding-top: 80px;
    color: rgb(252, 118, 162);

}

#myListInput {
    background-color: rgb(42, 62, 82);
    width: 800px;
    height: 50px;
    margin-bottom: 10px;
    color: rgb(252, 118, 162);
    font-size: 16px;
}

#myLyrics {
    padding: 50px 20px;
}

#btnShowMySavedSong {
    background-color: rgb(252, 118, 162);
    width: 500px;
    height: 40px;
    border: none;
    font-size: 16px;
    font-weight: bold;
    color: rgb(42, 62, 82);
    margin-top: 30px;
}

/* style for everything withing the lyrics and save functions */
#lyrics_area {
    color: rgb(66, 185, 132);
    padding: 60px 100px;
}

#btnSaveToMyList {
    background-color: rgb(252, 118, 162);
    width: 500px;
    height: 40px;
    border: none;
    font-size: 16px;
    font-weight: bold;
    color: rgb(42, 62, 82);
    margin-top: 30px;
}
</style>
