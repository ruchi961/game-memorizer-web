<template>
  <div id="mainClassPage">
    <div style="position:absolute;top:2%;left:39%;font-size:49px;color:darkgreen;text-shadow:2px 0px beige;background-color:beige;padding:10px; border-radius:30px 30px;">&#9989;Memorizer Game</div>
    <div class= "main">
      
      <input type="text" v-model="value1" class="numbersAssign" readonly @click="assignNumbers('value1')" v-on:keyup.enter="checkNumbers('1')" />
      <input type="text" v-model="value2" class="numbersAssign" readonly @click="assignNumbers('value2')" v-on:keyup.enter="checkNumbers('2')"/>
      <input type="text" v-model="value3" class="numbersAssign" readonly @click="assignNumbers('value3')" v-on:keyup.enter="checkNumbers('3')"/><br/>
      
      <input type="text" v-model="value4" class="numbersAssign" readonly @click="assignNumbers('value4')" v-on:keyup.enter="checkNumbers('4')"/>
      <input type="text" v-model="value5" class="numbersAssign" readonly @click="assignNumbers('value5')" v-on:keyup.enter="checkNumbers('5')"/>
      <input type="text" v-model="value6" class="numbersAssign" readonly @click="assignNumbers('value6')" v-on:keyup.enter="checkNumbers('6')"/><br/>
      
      <input type="text" v-model="value7" class="numbersAssign" readonly @click="assignNumbers('value7')" v-on:keyup.enter="checkNumbers('7')"/>     
      <input type="text" v-model="value8" class="numbersAssign" readonly @click="assignNumbers('value8')" v-on:keyup.enter="checkNumbers('8')"/>
      <input type="text" v-model="value9" class="numbersAssign" readonly @click="assignNumbers('value9')" v-on:keyup.enter="checkNumbers('9')"/>
      </div>
      
      <div class="rightBox">
        <span v-if="!enter && !statsGame"><button id="startBut" style="position:absolute;top:10%;left:38%;" @click="startgame()">{{startButText}}</button></span>
        <span v-if="enter">
         <div> 
          <h3 style="position:absolute;text-align:center;width:61%;text-wrap:break;left:18%;top:2%;background-color:beige;padding:10px;border-radius:30px;">{{this.phraseShow}}</h3>
          <input type="number" :value="textNo" readonly style="position:absolute;top:39%;left:38%;text-align:center;width:20%;padding:12px;font-size:30px;border-radius:10px 10px;outline:none;border:2px dashed green;"/>
          </div>
          </span>
          
          <span v-if="statsGame">
            <div>
              <span style="position:absolute;text-align:center;text-wrap:break;left:12%;top:15%;background-color:lightyellow;border-radius:10px 10px;font-size:20px;padding:10px;">&#9989;</span><h3 style="position:absolute;text-align:center;width:61%;text-wrap:break;left:23%;top:9%;background-color:lightyellow;border-radius:10px 10px;padding:19px;">The correctly answered blanks were: {{correctAnswer}}</h3>
              <span style="position:absolute;text-align:center;text-wrap:break;left:12%;top:52%;;background-color:rgb(252, 225, 225);border-radius:10px 10px;font-size:20px;padding:10px;">&#10060;</span><h3 style="position:absolute;text-align:center;width:61%;text-wrap:break;left:23%;top:46%;background-color:rgb(252, 225, 225);border-radius:10px 10px;padding:19px;"> The Wrongly answered blanks were: {{wrongAns}}</h3>
              <span style="position:absolute;text-align:center;text-wrap:break;left:12%;top:33%;background-color:bisque;border-radius:10px 10px;font-size:20px;padding:10px;">&#10134;</span> <h3 style="position:absolute;text-align:center;width:61%;text-wrap:break;left:23%;top:27%;background-color:bisque;border-radius:10px 10px;padding:19px;"> The unanswered blanks were: {{9 - (correctAnswer +wrongAns)}}</h3>
              <button @click="revealAnwser()" style="position:absolute;top:73%;left:19%;">Reveal Aswers</button>
              <button @click="restartGame()" style="position:absolute;top:73%;left:59%;">Restart</button>
              </div></span>

      </div>
  </div>

</template>
<script>
export default {
data(){
  return{
      /*value1:'\u2713',
      value2:"\u2717",
      value3:"\u274C",*/
      value1:'-',
      value2:"-",
      value3:"-",
      value4:"-",
      value5:"-",
      value6:"-",
      value7:"-",
      value8:"-",
      value9:"-",
      enter:false,
      startButText:"Start the game",
      textNo:30,
      enterelse:false,
      value_all:[],
      phraseShow:"",
      statsGame:false,
      correctAnswer:0,
      wrongAnswered:[0,0,0,0,0,0,0,0,0],
      wrongAns:0

  }
},
methods:{
  returnQuestion(val){
   
    if(val=="value1" && this.enterelse && this.value1==""){this.value1="?"}
  },
  assignNumbers(val=null){

if (val==null){
this.value1="?"
this.value2="?";;
this.value3="?"
this.value4="?"
this.value5="?"
this.value6="?"
this.value7="?"
this.value8="?"
this.value9="?"
}else{
  console.log( val,this.enterelse,document.getElementsByClassName("numbersAssign")[0].style.readonly)
 if(this.value1==""){this.value1="?"}
 else if(this.value2==""){this.value2="?"}
 else if(this.value3==""){this.value3="?"}
 else if(this.value4==""){this.value4="?"}
 else if(this.value5==""){this.value5="?"}
 else if(this.value6==""){this.value6="?"}
 else if(this.value7==""){this.value7="?"}
 else if(this.value8==""){this.value8="?"}
 else if(this.value9==""){this.value9="?"}

 if(val=="value1" && this.enterelse && this.value1!='\u2705'  && !this.statsGame){
    this.value1=""
    document.getElementsByClassName("numbersAssign")[0].removeAttribute("readonly")
    

  }else if(val=="value2" && this.enterelse && this.value2!='\u2705'  && !this.statsGame){
    this.value2=""
     document.getElementsByClassName("numbersAssign")[1].removeAttribute("readonly")


  }else if(val=="value3" && this.enterelse && this.value3!='\u2705'  && !this.statsGame){
   this.value3=""
   document.getElementsByClassName("numbersAssign")[2].removeAttribute("readonly")

   
  }else if(val=="value4" && this.enterelse && this.value4!='\u2705'  && !this.statsGame){
  
      this.value4=""
      document.getElementsByClassName("numbersAssign")[3].removeAttribute("readonly")

   
  }else if(val=="value5" && this.enterelse && this.value5!='\u2705'  && !this.statsGame){

      this.value5=""
       document.getElementsByClassName("numbersAssign")[4].removeAttribute("readonly")


  }else if(val=="value6" && this.enterelse && this.value6!='\u2705'  && !this.statsGame){

      this.value6=""
       document.getElementsByClassName("numbersAssign")[5].removeAttribute("readonly")



  }else if(val=="value7" && this.enterelse && this.value7!='\u2705'  && !this.statsGame){
      this.value7=""
       document.getElementsByClassName("numbersAssign")[6].removeAttribute("readonly")

      

  }else if(val=="value8" && this.enterelse && this.value8!='\u2705'  && !this.statsGame){
      this.value8=""
         document.getElementsByClassName("numbersAssign")[7].removeAttribute("readonly")


  }else if(val=="value9" && this.enterelse && this.value9!='\u2705'  && !this.statsGame){

      this.value9=""
      document.getElementsByClassName("numbersAssign")[8].removeAttribute("readonly")


  }
}
  },
startgame(){
 /* document.getElementsByClassName("numbersAssign")[0].style.backgroundColor="green";
 */
 
  document.getElementById("startBut").style.top="63%";
  this.enter=true;

  this.startButText="Stop the game"
  this.value1=Math.round(Math.random()*10);
  this.value2=Math.round(Math.random()*10);
  this.value3=Math.round(Math.random()*10);
  this.value4=Math.round(Math.random()*10);
  this.value5=Math.round(Math.random()*10);
  this.value6=Math.round(Math.random()*10);
  this.value7=Math.round(Math.random()*10);
  this.value8=Math.round(Math.random()*10);
  this.value9=Math.round(Math.random()*10);
  this.value_all.push(this.value1)
  this.value_all.push(this.value2)
  this.value_all.push(this.value3)
  this.value_all.push(this.value4)
  this.value_all.push(this.value5)
  this.value_all.push(this.value6)
  this.value_all.push(this.value7)
  this.value_all.push(this.value8)
  this.value_all.push(this.value9)

  this.ChangeTextNo()
  
   
},
async ChangeTextNo(){
this.phraseShow="Try to remember the numbers and their appropriate positions in 30 seconds"
while(this.textNo!=0){
await this.sleep(1000);
this.textNo = this.textNo -1
}
this.assignNumbers();

alert("Have you memorized?\nIts time to check!\nCClick on ok to continue")
this.enterelse=true
this.phraseShow="Please enter the numbers as you guess or remember, enter number and press enter key to evaluate"
this.textNo=60
while(this.textNo!=0){
await this.sleep(1000);
this.textNo = this.textNo -1
}
this.enter=false;
this.statsGame=true;
this.wrongAns=0;
for(var i =0; i<9;i++){
this.wrongAns = this.wrongAnswered[i] + this.wrongAns
}
console.log(this.wrongAnswered,this.wrongAns)
},
sleep(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}
,

subtract(){
  this.textNo = this.textNo - 1.0
  console.log(this.textNo)
  return
},
checkNumbers(pos_val){
  console.log(pos_val,this.value_all,this.value_all[0]==this.value1,this.value_all[0],this.value1)
  if(pos_val=="1"){
    
    if(this.value_all[0]==this.value1){
      document.getElementsByClassName("numbersAssign")[0].value=""
      this.correctAnswer=this.correctAnswer + 1
      this.value1="\u2705"
      console.log
    
    }else{
      this.wrongAnswered[0] = 1
      document.getElementsByClassName("numbersAssign")[0].value=""
      this.value1="\u274C"
    }
    document.getElementsByClassName("numbersAssign")[0].setAttribute('readonly','true')

  }else if(pos_val=="2"){
   
    if(this.value_all[1]==this.value2){
      document.getElementsByClassName("numbersAssign")[1].value=""
    this.correctAnswer=this.correctAnswer+1
        this.value2="\u2705"
    }else{
      this.wrongAnswered[1] = 1
      document.getElementsByClassName("numbersAssign")[1].value=""
        this.value2="\u274C"
        
    }
    document.getElementsByClassName("numbersAssign")[1].setAttribute('readonly','true')
  }else if(pos_val=="3"){
    
        if(this.value_all[2]==this.value3){
          document.getElementsByClassName("numbersAssign")[2].value=""
    this.correctAnswer=this.correctAnswer+1
        this.value3="\u2705"
    }else{
      this.wrongAnswered[2] = 1
      document.getElementsByClassName("numbersAssign")[2].value=""
        this.value3="\u274C"
    }
    document.getElementsByClassName("numbersAssign")[2].setAttribute('readonly','true')
  }else if(pos_val=="4"){
    
        if(this.value_all[3]==this.value4){
          document.getElementsByClassName("numbersAssign")[3].value=""
    this.correctAnswer=this.correctAnswer+1
        this.value4="\u2705"
    }else{
      this.wrongAnswered[3] = 1
      document.getElementsByClassName("numbersAssign")[3].value=""
        this.value4="\u274C"
    }
    document.getElementsByClassName("numbersAssign")[3].setAttribute('readonly','true')
  }else if(pos_val=="5"){
    
        if(this.value_all[4]==this.value5){
          document.getElementsByClassName("numbersAssign")[4].value=""
    this.correctAnswer=this.correctAnswer+1
        this.value5="\u2705"
    }else{
      this.wrongAnswered[4] = 1
      document.getElementsByClassName("numbersAssign")[4].value=""
        this.value5="\u274C"
    }
    document.getElementsByClassName("numbersAssign")[4].setAttribute('readonly','true')
  }else if(pos_val=="6"){
    
       if(this.value_all[5]==this.value6){
        document.getElementsByClassName("numbersAssign")[5].value=""
    this.correctAnswer=this.correctAnswer+1
        this.value6="\u2705"
    }else{
      this.wrongAnswered[5] = 1
      document.getElementsByClassName("numbersAssign")[5].value=""
        this.value6="\u274C"
    }
    document.getElementsByClassName("numbersAssign")[5].setAttribute('readonly','true')
  }else if(pos_val=="7"){
    document.getElementsByClassName("numbersAssign")[6].value=""
        if(this.value_all[6]==this.value7){
    this.correctAnswe=this.correctAnswer+1
        this.value7="\u2705"
    }else{
      this.wrongAnswered[6] = 1
      document.getElementsByClassName("numbersAssign")[6].value=""
        this.value7="\u274C"
    }
    document.getElementsByClassName("numbersAssign")[6].setAttribute('readonly','true')
  }else if(pos_val=="8"){
    
        if(this.value_all[7]==this.value8){
          document.getElementsByClassName("numbersAssign")[7].value=""
    this.correctAnswer=this.correctAnswer+1
        this.value8="\u2705"
    }else{
      this.wrongAnswered[7] = 1
      document.getElementsByClassName("numbersAssign")[7].value=""
        this.value8="\u274C"
    }
    document.getElementsByClassName("numbersAssign")[7].setAttribute('readonly','true')
  }else if(pos_val=="9"){
    
       if(this.value_all[8]==this.value9){
        document.getElementsByClassName("numbersAssign")[8].value=""
    this.correctAnswer=this.correctAnswer+1
        this.value9="\u2705"
    }else{
      this.wrongAnswered[8] = 1
      document.getElementsByClassName("numbersAssign")[8].value=""
        this.value9="\u274C"
    }
    document.getElementsByClassName("numbersAssign")[8].setAttribute('readonly','true')
  }

},
revealAnwser(){
  this.value1=this.value_all[0];
this.value2=this.value_all[1];
this.value3=this.value_all[2];
this.value4=this.value_all[3];
this.value5=this.value_all[4];
this.value6=this.value_all[5];
this.value7=this.value_all[6];
this.value8=this.value_all[7];
this.value9=this.value_all[8];
},
restartGame(){
  console.log(this.$router.push("/"))
this.$router.go(0)

}
}
}
</script>
<style>
html{
  height:100%;
  width:100%;
  background-color: aqua;

}
.numbersAssign{
width:16%;
text-align: center;
font-size:26px;
height:16%;
padding:10px;
border: 2px dashed green;
border-radius:32px 32px;
box-shadow: 2px 3px 9px 3px grey;
margin-left: 6%;
margin-bottom: 6%;
position: relative;
top:9%;
left:9.5%;

}
.numbersAssign:hover{
  background-color: #fdffc5;
  box-shadow: 0px 0px 21px 2px yellow;
}
#mainClassPage{
  position: absolute;
  top:0px;
  left:0px;
  width:100%;
  height:100%;
  background-color: chartreuse;
}

.main{
    position: absolute;
  top:18%;
  left:9%;
  width:41%;
  height:63%;
  background-color: rgb(56, 164, 37);
  box-shadow: 0px 0px 10px 5px rgb(33, 88, 11);
 
  
}
button{
  color:rgb(255, 255, 255);
  background-color: rgb(2, 44, 15);
  padding:10px;
  font-size:21px;
  box-shadow: 0px 0px 10px 2px grey;
  border-radius: 10px 10px;
  outline: none;
  border:2px solid rgb(4, 67, 4);
  text-align:center;
}
.rightBox{
  position: absolute;
  top:18%;
  left:55%;
  width:39%;
  height:63%;
  background-color: #ffffff26;
  border:2px solid rgb(236, 249, 177);
  box-shadow: 0px 0px 10px 2px grey;
}
</style>
