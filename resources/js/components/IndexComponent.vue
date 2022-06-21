<template>
<div class="wrap">
                <input type="button" id="start_button" value="start" v-on:click="ready()" style="text-align: center">
                <div id="count"></div>
                    <h1><div id="japanese"></div></h1>
                    <h2><div id="word"></div></h2>
                <div id="scoredis"></div>
    </div>
</template>

<script>
    export default {
        data: function () {
            return{
 wordlist : ["aaiebakouiu","isogabamaware","uogokoroarebamizugokoro","ennositanotikaramoti","oninomenimonamida","kaiinunitewokamareru","kyuusiniissyouwoeru","kutihawazawainomoto","geijutuhanagakujinseihamijikasi","koukaisakinitatazu","sarumokikaraotiru","siranugahotoke","suimoamaimokamiwaketa","zenhaisoge","daihasyouwokaneru","tirimotumorebayamatonaru","turuhasennenkamehamannen","tenhanibutuwoataezu","tokihakanenari","nagaimononihamakarero","nidoarukotohasandoaru","nukanikugi","nekonotemokaritai","norenniudeosi","hayaokihasanmonnotoku","hinonaitokoronikemurihatatanu","hukusuibonnikaerazu","benkeinonakidokoro","hotokenokaomosando","mayugewoyomareru","mikaradetasabi","musumehitorinimukohatinin","menihame,hanihaha","motonosayaniosamaru","yakeisinimizu","yudantaiteki","yowarimenitatarime","rakuhakunotane,kuharakunotane","ryouyakuhakutininigasi","ruihatomowoyobu","reiniyottereinogotosi","rongoyominorongosirazu","waraukadonihahukukitaru"],
 wordlistJapanese : ["ああ言えばこう言う","急がば回れ","魚心あれば水心","縁の下の力持ち","鬼の目にも涙","飼い犬に手を噛まれる","九死に一生を得る","口は禍の元","芸術は長く人生は短し","後悔先に立たず","猿も木から落ちる","知らぬが仏","酸いも甘いも噛み分けた","善は急げ","大は小を兼ねる","塵も積もれば山となる","鶴は千年亀は万年","天は二物を与えず","時は金なり","長い物には巻かれろ","二度あることは三度ある","糠に釘","猫の手も借りたい","暖簾に腕押し","早起きは三文の徳","火のないところに煙は立たぬ","覆水盆に反らず","弁慶の泣き所","仏の顔も三度","眉毛を読まれる","身から出た錆","娘一人に婿八人","目には目、歯には歯","元の鞘に納まる","焼け石に水","油断大敵","弱り目に祟り目","楽は苦の種、苦は楽の種","良薬は口に苦し","類は友を呼ぶ","例によって例の如し","論語読みの論語知らず","笑う門には福来たる"],
      time_limit : 90,
      readytime : 3,
      score:0,
      correct:0,
      mistake:0,
      char_num : 0,
      word_char:"",
      random:0,
            };
        },
        mounted() {
            document.onkeydown = function(e) {
    if(e.keyCode == 189){
       keyStr = "-";
       }else if(e.keyCode == 188){
                keyStr = ","
                }else{
 var keyStr = String.fromCharCode(e.keyCode);
    keyStr = keyStr.toLowerCase();
       }
    if(keyStr == this.word_char){
        word.innerHTML="<span style='color: red;'>"+this.wordlist[this.random].substr(0,this.char_num+1)+"</span>"+this.wordlist[this.random].substr(this.char_num+1,this.wordlist[this.random].length);
        this.char_num++;
        this.correct++;
        this.charInsort();
       }else{
           this.mistake++;
       }
    if(this.char_num == this.wordlist[this.random].length){
        this.char_num=0;
        this.wordDisplay();
       }
}.bind(this);
        },
        methods:{
    ready(){
         this.readytime = 3;
         scoredis.innerHTML="";
         start_button.style.visibility ="hidden";
         var readytimer = setInterval(function(){
             count.innerHTML=this.readytime;
             this.readytime--;
             if(this.readytime < 0){
                clearInterval(readytimer);
                 this.gameStart();
                }
         }.bind(this),1000);
     },
     gameStart(){
         this.score = 0.0;
         this.mistake = 0;
         this.correct = 0;
         this.wordDisplay();
         var time_remaining = this.time_limit;
         var gametimer = setInterval(function(){
            count.innerHTML="残り時間："+time_remaining;
             time_remaining--;
             if(time_remaining <= 0){
             clearInterval(gametimer);
                 this.finish();
         }
         }.bind(this),1000);
     },
     wordDisplay(){
         this.random = Math.floor( Math.random() * this.wordlist.length );
         word.innerHTML=this.wordlist[this.random];
         japanese.innerHTML=this.wordlistJapanese[this.random];
         this.charInsort();
     },
     charInsort(){
         this.word_char = this.wordlist[this.random].charAt(this.char_num);
     },
     finish(){
         this.score = Math.floor(Math.pow(this.correct,2) * Math.pow((this.correct/(this.correct+this.mistake)),5));
         scoredis.innerHTML="スコア:"+this.score+"点"+"<hr>正タイプ数:"+this.correct+"<br>ミスタイプ数:"+this.mistake+"<br>正答率"+(this.correct/(this.correct+this.mistake)*100).toFixed(1)+"%";
         count.innerHTML="";
         word.innerHTML="";
         japanese.innerHTML="";
         start_button.style.visibility ="visible";
         this.word_char=0;
         this.random = 0;
         this.char_num = 0;
     },

        }
    }
</script>

<style>
.wrap{
     text-align:center;
}
</style>
