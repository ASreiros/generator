<template>
    <div class="generator-df">
        <Head title="Difficulty calculator"></Head>
        <div class="difGenerator-main">
            <!-- Player container -->
            <div  class="dg-left">
                <div v-for="index in playerLines" :key="index" class="dg-left-generator">
                    <div class="dg-left-holder">
                        <div class="small-container">
                            <label for="plvl">Player lvl</label>
                            <input id="plvl" name="plvl" type="number" min="1" max="20">
                        </div>
                        <div class="small-container">
                            <label for="pnr">Player number</label>
                            <input id="pnr" name="pnr" type="number" min="1">
                        </div>
                    </div>
                </div>
                <div class="btn-container">
                    <SmallButton @clicked="addPlayerLine" text="add line"></SmallButton>
                    <SmallButton @clicked="removePlayerLine" text="remove line"></SmallButton>
                </div> 
            </div>  

            <!-- Opponent container -->

            <div  class="dg-left">
                <div v-for="index in opponentLines" :key="index" class="dg-left-generator">
                    <div class="dg-left-holder">
                        <div class="small-container">
                            <label for="ocr">Opponent CR</label>
                            <input id="ocr" name="ocr" type="text" min="1" max="20">
                        </div>
                        <div class="small-container">
                            <label for="onr">Opponent number</label>
                            <input id="onr" name="onr" type="number">
                        </div>
                    </div>
                </div>
                <div class="btn-container">
                    <SmallButton @clicked="addOpponentLine" text="add line"></SmallButton>
                    <SmallButton @clicked="removeOpponentLine" text="remove line"></SmallButton>
                </div> 
            </div>  
        </div>
        <div id="info-block" class="info-block">
            
        </div>
        <div>
            <SmallButton @clicked="calculate" text="Calculate diffculty"></SmallButton>
        </div>
        
    </div>
</template>

<script>

import Head from './parts/Head.vue';
import SmallButton from './parts/SmallButton.vue';
    export default {
    components: { Head, SmallButton },

    data(){
      return{
        playerLines:1,
        opponentLines:1,
        playerE:[0,25,50,75,125,250,300,350,450,550,600,800,1000,1100,1250,1400,1600,2000,2100,2400,2800],
        playerM:[0,50,100,150,250,500,600,750,900,1100,1200,1600,2000,2200,2500,2800,3200,3900,4200,4900,5700],
        playerH:[0,75, 150, 225, 375, 750, 900, 1100, 1400, 1600, 1900, 2400, 3000, 3400, 3800, 4300, 4800, 5900, 6300, 7300, 8500],
        playerD:[0, 100, 200, 400, 500, 1100, 1400, 1700, 2100, 2400, 2800, 3600, 4500, 5100, 5700, 6400, 7200, 8800, 9500, 10900, 12700],
        playerEP:[0, 150, 300, 600, 750, 1650, 2100, 2550, 3150, 3600, 4200, 5400, 6750, 7650, 8550, 9600, 10800, 13200, 14250, 16350, 19050],
        cr:{
            "0":10,
            "1/8":25,
            "1/4":50,
            "1/2":100,
            "1":200,
            "2":450,
            "3":700,
            "4":1100,
            "5":1800,
            "6":2300,
            "7":2900,
            "8":3900,
            "9":5000,
            "10":5900,
            "11":7200,
            "12":8400,
            "13":10000,
            "14":11500,
            "15":13000,
            "16":15000,
            "17":18000,
            "18":20000,
            "19":22000,
            "20":25000,
            "21":33000,
            "22":41000,
            "23":50000,
            "24":62000,
            "25":75000,
            "26":89000,
            "27":104000,
            "28":120000,
            "29":137000,
            "30":155000,
        },

        multiplier:[0,1,1.5,2,2,2,2,2.5,2.5,2.5,2.5,3,3,3,3,4]
      }
    },

    methods:{
        addPlayerLine(){
            this.playerLines++;
        },

        removePlayerLine(){
            if(this.playerLines>1){
                this.playerLines--;
            }  
        },

        addOpponentLine(){
            this.opponentLines++;
        },

        removeOpponentLine(){
            if(this.opponentLines>1){
                this.opponentLines--;
            }  
        },

        calculate(){
            let error = "";
            let pnrArr =  document.querySelectorAll('#pnr')
            let pnr = [];
            pnrArr.forEach(n=>{
                const number = Number(n.value);
                if ((typeof(number)==="number")&&(number > 0)&&(Math.floor(number)===number)&&(number<11)) {
                    pnr.push(number)
                } else{
                error += `<p>Please enter number of players between 1 and 10 per line. Please enter positive, full number of players. Number of players ${number} is incorrect.</p>` 
                }
            })  

            let plvlArr =  document.querySelectorAll('#plvl')
            let plvl = [];
            plvlArr.forEach(n=>{
                const number = Number(n.value);
                if ((typeof(number)==="number")&&(number > 0)&&(Math.floor(number)===number)&&(number<20)) {
                    plvl.push(number)
            } else{
                error += `<p>Please enter lvl of players between 1 and 20. Please enter positive, full number as lvl.  ${number} lvl is incorrect.<p>` 
            }
            })

            let onrArr =  document.querySelectorAll('#onr')
            let onr = [];
            onrArr.forEach(n=>{
                const number = Number(n.value);
                if ((typeof(number)==="number")&&(number > 0)&&(Math.floor(number)===number)&&(number<51)) {
                    onr.push(number)
                } else{
                error += `<p>Please enter number of opponents between 1 and 50 per line. Please enter positive, full number of opponents. Number of opponents ${number} is incorrect.</p>` 
                }
            })

            let ocrArr =  document.querySelectorAll('#ocr')
            let ocr = [];
            ocrArr.forEach(n=>{
                if (this.cr[n.value]) {
                    ocr.push(this.cr[n.value])
                } else{
                error += `<p>Please enter valid CR. Examples of valid CR are 1/8, 1/4, 1/2, 1, 2, 3, ... 30. CR ${n.value} is incorrect.</p>` 
                }
            })
            let info = "";

            if(error === ""){

                let treshold ={
                    easy:0,
                    medium:0,
                    hard:0,
                    deadly:0,
                    epic:0
                }

                for (let i = 0; i < plvl.length; i++)  {
                    treshold.easy += this.playerE[plvl[i]]*pnr[i];
                    treshold.medium += this.playerM[plvl[i]]*pnr[i];
                    treshold.hard += this.playerH[plvl[i]]*pnr[i];
                    treshold.deadly += this.playerD[plvl[i]]*pnr[i];
                    treshold.epic += this.playerEP[plvl[i]]*pnr[i];
                }

                let expBasic = 0;
                let nrOfOpponents = 0;
                
                for (let i = 0; i < ocr.length; i++) {
                    expBasic += ocr[i] * onr[i];
                    nrOfOpponents += onr[i];
                }

                let multpl= 4;

                if(nrOfOpponents < 16){
                    multpl= this.multiplier[nrOfOpponents]
                }

                let expMultiple = expBasic * multpl;
                let danger = "";

                if(expMultiple < treshold.easy){
                    danger = "trivial"
                }
                if(expMultiple > treshold.easy){
                    danger = "easy"
                }
                if(expMultiple > treshold.medium){
                    danger = "medium"
                }
                if(expMultiple > treshold.hard){
                    danger = "hard"
                }
                if(expMultiple > treshold.deadly){
                    danger = "deadly"
                }
                if(expMultiple > treshold.epic){
                    danger = "impossible"
                }

                info = `<p> Treshold for this party are following:</p>
                <ul>
                    <li>Easy difficulty:${treshold.easy} exp</li>
                    <li>Medium difficulty:${treshold.medium} exp</li> 
                    <li>Hard difficulty:${treshold.hard} exp</li> 
                    <li>Deadly difficulty:${treshold.deadly} exp</li>
                    <li>Imposible difficulty:${treshold.epic} exp</li>          
                </ul>
                <p>This opponents exp value ${expBasic}.</p>
                <p>This opponents exp value after adjustment for size ${expMultiple}.</p>
                <p>This skirmish final difficulty is  <span style="color:red; text-transform:uppercase">${danger}</span>.</p>
                
                `

                console.log(pnr);
                console.log(plvl);
                console.log(ocr);
                console.log(onr);
                console.log(treshold);
                console.log(expBasic);
                console.log(expMultiple);
            } else{
                info = error;
            }
            document.querySelector('#info-block').innerHTML = info;
        }
    }

}
</script>

<style lang="scss" scoped>
    .generator-df{
        display: flex;
        flex-wrap: wrap;
        flex-direction: column;
        width: 100%;
        justify-content: flex-start;
        gap: 20px;
        align-items: center;


    }

    .difGenerator-main{
        width: 80%;
        margin: 0 auto;
        display: flex;
        flex-direction: row;
        justify-content:space-around;
        flex-wrap: wrap;
        gap: 20px;

    }

    .dg-left{
        display: flex;
        flex-direction: column;
        gap: 20px;

        .dg-left-holder{
            display: flex;
            flex-direction: row;
            gap: 30px;
        }

        .btn-container{
            width: 100%;
            display: flex;
            flex-direction: row;
            gap: 20px;
        }


    }
    .small-container{
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        align-items: flex-start;

        label{
            font-size: 24px;
        }

        input{
            color: rgb(95, 247, 95);
            background-color: rgb(46, 44, 44);
            border: double 3px rgb(95, 247, 95);
            width: 250px;
            height: 30px;
            font-size: 24px;
            line-height: 30px;
            
        }
    }
</style>