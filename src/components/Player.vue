<template>
    <div class="wrapper-player">
        <div class="player-panel winner">
            <div class="player-name">Winner</div>
            <div class="player-score">43</div>
            <div class="player-current-box">
            <div class="player-current-label">Current</div>
            <div class="player-current-score">11</div>
            </div>
        </div>

        <div class="player-panel">
            <div class="player-name">Player 2</div>
            <div class="player-score">72</div>
            <div class="player-current-box">
            <div class="player-current-label">Current</div>
            <div class="player-current-score">0</div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'players',
    data() {
        return {
            
        }
    }
}
</script>

<style>

.player-panel {
    width: 50%;
    float: left;
    height: 600px;
    padding: 100px;
    transition: all 0.3s ease;
    background-color: #fff;
}
.player-name {
    font-size: 40px;
    text-align: center;
    text-transform: uppercase;
    letter-spacing: 2px;
    font-weight: 100;
    margin-top: 20px;
    margin-bottom: 10px;
    position: relative;
}

.player-score {
    text-align: center;
    font-size: 80px;
    font-weight: 100;
    color: #42b983;
    margin-bottom: 130px;
}

.active {
    background-color: #f7f7f7;
}
.active .player-name {
    font-weight: 300;
}

.active .player-name::after {
    content: "\2022";
    font-size: 47px;
    position: absolute;
    color: #42b983;
    top: -7px;
    right: 10px;
}

.player-current-box {
  background-color: #42b983;
  color: #fff;
  width: 40%;
  margin: 0 auto;
  padding: 12px;
  text-align: center;
}

.player-current-label {
  text-transform: uppercase;
  margin-bottom: 10px;
  font-size: 12px;
  color: #222;
}

.player-current-score {
  font-size: 30px;
}

.winner {
  background-color: #f7f7f7;
}
.winner .player-name {
  font-weight: 300;
  color: #42b983;
}

</style>