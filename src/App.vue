<template>
    <div id="app">
        <div class="wrapper clearfix">
        
        <Players 
            v-bind:scorePlayer="scorePlayer"
            v-bind:currentScore="currentScore"
            v-bind:activePlayer="activePlayer"
        />

        <Control
            v-on:handleRollDice="handleRollDice"
            v-on:handleNewGame="handleNewGame"
        />

        <Dice
            v-bind:dices="dices"
        />

        <PopupRule
            v-on:confirmEvent="confirmEvent"
            v-bind:isOpenPopup="isOpenPopup"
        />

        </div>
    </div>
</template>

<script>

import Players from './components/Player'
import Control from './components/Control'
import Dice from './components/Dice' 
import PopupRule from './components/PopupRule'

export default {
    name: "App",
    data () {
        return {
            isPlaying: false,
            isOpenPopup: false,
            dices: [1, 5],
            activePlayer: 1,
            currentScore: 30,
            scorePlayer: [13, 30]
        } 
    },
    components: {
        Players,
        Control,
        Dice,
        PopupRule
    },
    methods: {
        nextPlayer() {
            this.activePlayer = this.activePlayer === 0 ? 1 : 0
            this.currentScore = 0
        },
        handleRollDice() {
            if(this.isPlaying) {
                var dice1 = Math.floor(Math.random() * 6) + 1;
                var dice2 = Math.floor(Math.random() * 6) + 1;

                this.dices = [dice1, dice2]

                if(dice1 == 1 || dice2 == 1) {
                    this.nextPlayer()
                } else {
                    this.currentScore = this.currentScore + dice1 + dice2;
                }
            } else {
                alert('Please click on New Game Button for a new game :D')
            }
        },
        handleNewGame() {
            this.isOpenPopup = true;
        },
        confirmEvent() {
            this.isPlaying = true;
            this.isOpenPopup = false;
            this.activePlayer = 0
            this.currentScore = 0
            this.scorePlayer = [0, 0]
        },
    }
};
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.clearfix::after {
    content: "";
    display: table;
    clear: both;
}

body {
    background-image: linear-gradient(
        rgba(62, 20, 20, 0.4),
        rgba(62, 20, 20, 0.4)
        ),
        url("/assets/back.jpg");
    background-size: cover;
    background-position: center;
    font-family: Lato;
    font-weight: 300;
    position: relative;
    height: 100vh;
    color: #555;
}

.wrapper {
    width: 1000px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: #fff;
    box-shadow: 0px 10px 50px rgba(0, 0, 0, 0.3);
    overflow: hidden;
}

</style>