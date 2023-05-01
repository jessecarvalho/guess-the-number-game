<template>
    <div class="alert-modal">
        <div class="intern-alert-modal">
            <span id="close" @click="closeModal">Close</span>
            <h2></h2>
        </div>
    </div>
    <div class="main-game">
        <div class="grid">
            <div class="col">
                <div id="celphone">
                    <div id="phone-cameras">
                        <div class="small-camera"></div>
                        <div class="small-camera"></div>
                        <div class="big-camera"></div>
                    </div>
                    <div id="phone-screen">
                        <div id="intern-phone-screen">

                            <div class="result">
                                <h3></h3>
                                <img src="" alt="">
                            </div>

                            <div class="screen-game">

                                <div id="tries">
                                    <div class="try"></div>
                                    <div class="try"></div>
                                    <div class="try"></div>
                                    <div class="try"></div>
                                    <div class="try"></div>
                                    <div class="try"></div>
                                    <div class="try"></div>
                                </div>
                                <div id="current-number">
                                    <span>
                                        {{ current }}
                                    </span>
                                </div>
                                <div>
                                    <h2 id="hint"> </h2>
                                </div>
                                <div id="keyboard">
                                    <div class="grid">
                                        <div class="col">
                                            <div class="key" data-key="1">
                                                <span>
                                                    1
                                                </span>
                                            </div>
                                        </div>
                                        <div class="col">
                                            <div class="key" data-key="2">
                                                <span>
                                                    2
                                                </span>
                                            </div>
                                        </div>
                                        <div class="col">
                                            <div class="key" data-key="3">
                                                <span>
                                                    3
                                                </span>
                                            </div>
                                        </div>
                                    </div>
                                    <div class="grid">
                                        <div class="col">
                                            <div class="key" data-key="4">
                                                <span>
                                                    4
                                                </span>
                                            </div>
                                        </div>
                                        <div class="col">
                                            <div class="key" data-key="5">
                                                <span>
                                                    5
                                                </span>
                                            </div>
                                        </div>
                                        <div class="col">
                                            <div class="key" data-key="6">
                                                <span>
                                                    6
                                                </span>
                                            </div>
                                        </div>
                                    </div>
                                    <div class="grid">
                                        <div class="col">
                                            <div class="key" data-key="7">
                                                <span>
                                                    7
                                                </span>
                                            </div>
                                        </div>
                                        <div class="col">
                                            <div class="key" data-key="8">
                                                <span>
                                                    8
                                                </span>
                                            </div>
                                        </div>
                                        <div class="col">
                                            <div class="key" data-key="9">
                                                <span>
                                                    9
                                                </span>
                                            </div>
                                        </div>
                                    </div>
                                    <div class="grid">
                                        <div class="col">
                                            <div class="key" data-key="clear">
                                                <span>
                                                    Clear
                                                </span>
                                            </div>
                                        </div>
                                        <div class="col">
                                            <div class="key" data-key="0">
                                                <span>
                                                    0
                                                </span>
                                            </div>
                                        </div>
                                        <div class="col">
                                            
                                        </div>
                                    </div>
                                </div>
                                
                            </div>

                            
                        </div>
                    </div>
                    <div>
                        <button id="button-check" @click="checkNumber">
                            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path d="M438.6 105.4c12.5 12.5 12.5 32.8 0 45.3l-256 256c-12.5 12.5-32.8 12.5-45.3 0l-128-128c-12.5-12.5-12.5-32.8 0-45.3s32.8-12.5 45.3 0L160 338.7 393.4 105.4c12.5-12.5 32.8-12.5 45.3 0z"/></svg> Check
                        </button>
                        <button id="button-try-again" @click="playAgain">
                            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path d="M438.6 105.4c12.5 12.5 12.5 32.8 0 45.3l-256 256c-12.5 12.5-32.8 12.5-45.3 0l-128-128c-12.5-12.5-12.5-32.8 0-45.3s32.8-12.5 45.3 0L160 338.7 393.4 105.4c12.5-12.5 32.8-12.5 45.3 0z"/></svg> Play Again
                        </button>
                    </div>
                </div>
            </div>
            <div class="col">
                <div class="text">
                    <h1>Guess the number to unlock the phone</h1>
                    <hr>
                    <p>Pick a number from 0 to 100 and you have 10 chances to unlock this phone. <br /> Use the hints to win the game</p>
                </div>
                
            </div>
        </div>
    </div>
</template>

<script>

    export default {
        methods: {
            keyPress(key) {
                if (key === "clear") {
                    this.current = 0;
                } else if (this.current == 0) {
                    this.current = key;
                } else {
                    if (this.current.length == 3) {
                        this.openModal();
                    } else {
                        this.current += key;
                    }
                }
            },
            openModal() {
                const modal = document.querySelector('.alert-modal');
                modal.querySelector(':scope > div > h2').innerHTML = "You can only write 3 numbers";
                modal.style.display = "flex";
            },
            closeModal() {
                const modal = document.querySelector('.alert-modal');
                modal.querySelector(':scope > div > h2').innerHTML = ""
                modal.style.display = "none";
            },
            drawANumber() {
                this.drawnNumber = Math.floor(Math.random() * 101);
            },
            checkNumber() {
                let hint = document.querySelector('#hint');
                if (this.current == this.drawnNumber) {
                    hint.innerHTML = "";
                    this.endGame(0);
                } else if (this.current > this.drawnNumber) {
                    hint.innerHTML = "Its minor than: " + this.current;
                } else if(this.current < this.drawnNumber) {
                    hint.innerHTML = "Its bigger than: " + this.current;
                }

                this.current = 0;
                this.showAttempts();
            },
            showAttempts() {
                var tryEl = document.querySelectorAll('.try');
                if (this.attempts == 7 ) {
                    this.endGame(1);
                } 
                else {
                    this.attempts++;
                    tryEl = document.querySelectorAll('.try');
                    for (var i = 0; i< this.attempts; i++) {
                        tryEl[i].style.backgroundColor = "#000";
                    }
                }
            }, 
            cleanAttempts() {
                var tryEl = document.querySelectorAll('.try');
                for (var j = 0; j < 7; j++) {
                    tryEl[j].style.backgroundColor = "#fff";
                }
            }, 
            endGame(result){

                var resultEl = document.querySelector('.result');
                var screenGameEl = document.querySelector('.screen-game');
                var buttonCheckEl = document.querySelector('#button-check');
                var buttonTryAgainEl = document.querySelector('#button-try-again');
                var gifNumber = (Math.floor(Math.random() * 10) + 1);
                resultEl.style.display = "block";
                buttonCheckEl.style.display = "none";
                screenGameEl.style.display = "none";
                buttonTryAgainEl.style.display = "inline";

                if(result == 0) {
                    resultEl.querySelector(':scope > h3').innerHTML = "Yeaa you nailed this game";
                    resultEl.querySelector(':scope > img').setAttribute('src', './src/assets/imgs/won-' + gifNumber + '.gif');
                } else {
                    resultEl.querySelector(':scope > h3').innerHTML = "Omg you lose it";
                    resultEl.querySelector(':scope > img').setAttribute('src', './src/assets/imgs/lose-' + gifNumber + '.gif');
                }
            },
            playAgain() {
                var resultEl = document.querySelector('.result');
                var screenGameEl = document.querySelector('.screen-game');
                var buttonCheckEl = document.querySelector('#button-check');
                var buttonTryAgainEl = document.querySelector('#button-try-again');
                resultEl.style.display = "none";
                buttonCheckEl.style.display = "inline";
                screenGameEl.style.display = "block";
                buttonTryAgainEl.style.display = "none";
                this.current = 0;
                this.attempts = 0;
                console.log(this.attempts);
                this.drawANumber();
                this.cleanAttempts();
            },
        },
        mounted() {
            var keys = document.querySelectorAll('.key');
            for (let i = 0; i < keys.length; i++) {
                keys[i].addEventListener('click', () => this.keyPress(keys[i].dataset.key));
            }
            this.drawANumber();
        },
        data() {
            return {
                current : 0,
                drawnNumber : 0,
                attempts : 0,
            }
        },
    }

</script>