<template>
    <div id="app">
        <div class="wrapper clearfix">
        
        <Players 
            v-bind:isWinner="isWinner"
            v-bind:scorePlayer="scorePlayer"
            v-bind:currentScore="currentScore"
            v-bind:activePlayer="activePlayer"
        />

        <Control
            v-bind:isPlaying="isPlaying"
            v-bind:finalScore="finalScore"
            v-on:handleChangeFinalScore="handleChangeFinalScore"
            v-on:handleRollDice="handleRollDice"
            v-on:handleNewGame="handleNewGame"
            v-on:handleHoldScore="handleHoldScore"
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
            dices: [0, 0],
            activePlayer: 0,
            currentScore: 0,
            scorePlayer: [0, 0],
            finalScore: 10
        } 
    },
    components: {
        Players,
        Control,
        Dice,
        PopupRule
    },
    computed: {
        // function auto run when data inside changed
        isWinner: function () {
            let { scorePlayer, finalScore } = this;
            if(scorePlayer[0] >= finalScore || scorePlayer[1] >= finalScore ) {
                return true;
            }
            return false;
        }
    },
    watch: {
        isWinner: {
            deep: true,
            handler: function(val) {
                this.isPlaying = (val) ? false : true;
            }
        }
    },
    methods: {
        handleChangeFinalScore: function(number) {
            number = parseInt(number)
            if(isNaN(number)) {
                this.finalScore = '';
            } else {
                this.finalScore = number
            }
        }, 
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
        handleHoldScore: function() {
            if(this.isPlaying) {
                let { scorePlayer, activePlayer, currentScore } = this;
                let scoreOld = scorePlayer[activePlayer];
                // let cloneScorePlayer = [...scorePlayer];
                this.$set(this.scorePlayer, activePlayer, scoreOld + currentScore);

                if(!this.isWinner) {
                    this.nextPlayer(); 
                }
            } else {
                alert('Please, click on New Game button for a New Game')
            }
        }
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