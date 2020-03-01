<template>
    <div class="card">
        <div class="inner-card" v-bind:style="{'background-color': colours()}">
            <div class="gradient" v-bind:style="{'background-color': colours()}"></div>
            <div class="image">
                <img v-if="health>=90" class="bg-image sparkle" src="../CardBasic/sparkle.gif">
                <div v-else class="bg-image sparkle"></div>
                <img class="bg-image pokemon" :src="require('../pokemon/images/' +imageUrl+'.png')">
                <div class="header">
                    <h1>{{title}}</h1>
                    <h2>{{health}} HP</h2>
                </div>
            </div>
            <div class="text">
                <span class="banner">Pokémon No.{{imageUrl}}</span>
                <p style="font-weight:700; color:#000000; text-shadow:0px 2px 5px #00000055;">
                    <span style="opacity:0.75;">- Pokemon Type - </span><br><br>
                    <span>
                        <span style="border:4px solid #fff6; box-shadow:inset 0px 0px 10px #fff6, 0px 5px 10px #0008; background-image:linear-gradient(50deg, #fff0 60%, #fff8 70%, #fff0 95%); padding:5px 10px 7px 10px; border-radius:50px;" v-bind:style="{'background-color' : lookUpColour().colours1[0]}">
                        {{varType1}}</span>
                        <span style="text-align:centre;" v-if="varTypeLength === 2">
                        <span style="color:#000000; opacity:0.75;padding:0px 5px;"> &</span> <span style="border:4px solid #fff6; box-shadow:inset 0px 0px 10px #fff6, 0px 5px 10px #0008; background-image:linear-gradient(50deg, #fff0 60%, #fff8 70%, #fff0 95%); padding:5px 10px 7px 10px; border-radius:50px;" v-bind:style="{'background-color' : lookUpColour().colours2[1]}">{{varType2}}</span>
                        </span>
                    </span>
                </p>
            </div>
        </div>
    </div>
</template>

<style scoped>
    .card > *{pointer-events: none;}
    .inner-card{
        position: relative;
        margin:0 auto;
        top:20px;
        width:275px;
        height:400px;
        background: #ff3300 url('../CardBasic/smoke.png') no-repeat bottom;
        overflow:hidden;
    }
    .gradient{
        width:215px;
        height:150px;
        position: relative;
        top:40px;
        margin:0 auto;
        opacity: 0.5;
        background-size: auto 100%;
        background-clip: padding-box;
        border:#0000 10px;
    }
    .image{
        width:215px;
        height:150px;
        position: relative;
        top:-120px;
        margin:0 auto;
        background-size: auto 80%, 100% 100%;
        background-clip: padding-box;
        border:#ffff0080 groove 10px;
    }
    .image .bg-image{height: 100%; position: relative;display: block; margin:0 auto !important;}
    .pokemon{top:-90%; height:80% !important;}
    .sparkle{width:100%;}
    .header{
        position: relative;
        top: -180%;
    }
    h1{
        margin: 0px;
        padding: 0px;
        position: relative;
        top: -40px;
        font-size: 24px;
        left: -5px;
        display: inline;
        text-shadow:0px 2px 5px #00000055;
    }
    h2{
        margin: 0px;
        padding: 0px;
        position: relative;
        top: -40px;
        font-size: 24px;
        left: -5px;
        display: inline;
        color: #d00;
        text-align: end;
        font-weight: 400;
        float: right;
        text-shadow:0px 0px 5px #fff9;
    }
    h3{
        display:inline;
        color:#858 !important;
        text-shadow:0px 2px 5px #00000055;
    }

    .text{
        height: 50%;
        position: relative;
        top: -30%;
        width:80%;
        margin: 0 auto;
    }
    .banner{
        display: block;
        text-align: center;
        font-style: italic;
        background-image: linear-gradient(50deg,
        #a80 0%, #fd6 50%,
        #a80 100%);
        margin-top: 5px;
        font-size: 9.5px;
        border-radius: 5px;
        font-weight: 600;
        text-shadow:0px 2px 5px #00000055;
        box-shadow:0px 5px 5px #00000055;
    }
</style>

<script>
const colorList = require("../pokemon/typesColours.json");
var imageUrl;
export default {
    props:{
        title: String,
        health: Number,
        type: Array,
        image: Number
    },
    name: "Pokemon",
    data(){
        return {
            imageUrl: ('000' + this.image).slice(-3),
            varTypeLength: this.type.length,
        


            //TypeColours:
            varType1Light: (this.type[0]+" light"),
            varType1: (this.type[0]),
            varType1Dark: (this.type[0]+" dark"),
            varType2Light: (this.type[1]+" light"),
            varType2: (this.type[1]),
            varType2Dark: (this.type[1]+" dark")
        };
    },
    methods:{
        lookUpColour(){
                    var colours1 = [];
                    var colours2 = [];
            //Only change code below this line
            for(var i =0;i<colorList.length;i++){
                if (colorList[i].type.toUpperCase() === this.varType1Light.toUpperCase()){
                    colours1.push("#" + colorList[i]["code"])
                }
                if (colorList[i].type.toUpperCase() === this.varType1.toUpperCase()){
                    colours1.push("#" + colorList[i]["code"])
                }
                if (colorList[i].type.toUpperCase() === this.varType1Dark.toUpperCase()){
                    colours1.push("#" + colorList[i]["code"])
                }
                if(this.varTypeLength > 1){
                    if (colorList[i].type.toUpperCase() === this.varType2Light.toUpperCase()){
                        colours2.push("#" + colorList[i]["code"])
                    }
                    if (colorList[i].type.toUpperCase() === this.varType2.toUpperCase()){
                        colours2.push("#" + colorList[i]["code"])
                    }
                    if (colorList[i].type.toUpperCase() === this.varType2Dark.toUpperCase()){
                        colours2.push("#" + colorList[i]["code"])
                    }
                }
            }
            return {colours1, colours2}
        },
        colours(){
            function hexToRgb(hex) {
                var result = /^#?([a-f\d]{2})([a-f\d]{2})([a-f\d]{2})$/i.exec(hex);
                return result ? {
                    r: parseInt(result[1], 16),
                    g: parseInt(result[2], 16),
                    b: parseInt(result[3], 16)
                } : null;
            }
            let red = 0;
            let green = 0;
            let blue = 0;
            var hexRed = "";
            var hexGreen = "";
            var hexBlue = "";

            var colour1 = this.lookUpColour().colours1[1];
            var colour2 = this.lookUpColour().colours2[1];


            //Returns base colour if there is no extra type
            if(this.varTypeLength < 2){return colour1;}


            /*Holds string of colour returned*/
            /*Converts hex value from "typesColours.json" to decimal values and calculates a mean hex colour for the card background*/ 

            //Colour1
            else{
                red   += hexToRgb(colour1).r;
                green += hexToRgb(colour1).g;
                blue  += hexToRgb(colour1).b;

                red   += hexToRgb(colour1).r;
                green += hexToRgb(colour1).g;
                blue  += hexToRgb(colour1).b;

                //Colour2
                red   += Math.round(hexToRgb(colour2).r*0.75);
                green += Math.round(hexToRgb(colour2).g*0.75);
                blue  += Math.round(hexToRgb(colour2).b*0.75);

                hexRed = Math.round(red/3);
                hexGreen = Math.round(green/3);
                hexBlue = Math.round(blue/3);

             

                function rgbToHex() {
                return "#" + ((1 << 24) + (hexRed << 16) + (hexGreen << 8) + hexBlue).toString(16).slice(1);
            }
                return rgbToHex();
                }
            },
    }
};
</script>