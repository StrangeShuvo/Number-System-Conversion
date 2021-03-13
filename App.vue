<template>
    <div id="app">
     
    <div class ="container">
        <!-- Header section -->
        <header id="title">
            <h1>Nano Converter</h1>
        </header>
        <section>
        <!-- Main content section -->
        
            <!-- Number System cinversion -->
            
                <h2>Number System Conversion</h2>
                <div class="box">
                <div class="input-group">
                <label >Decimal</label>
                <input type="text" placeholder="input any decimal number,eg.33233"
                v-model="numbers.decimal"
                />
                

            </div>
            <div class="input-group">
                <label >Binary</label>
                <input type="text" placeholder="input any Binary number,eg.011110"
                v-model="numbers.binary"
                />
                 

            </div>
            <div class="input-group">
                <label >Octal</label>
                <input type="text" placeholder="input any Octal number, eg. 1777"
                v-model="numbers.octal"
                />
                 

            </div>
            <div class="input-group">
                <label >HexaDecimal</label>
                <input type="text" placeholder="input any HexaDecimal number,eg.AC147"
                v-model="numbers.hexadecimal"
                />
                 

            </div>
            <div class ="reset-btn-container">
            <p v-if="invalidNumber" style="color: red;">
            Invalid input
            </p>
                <button  @click="resetNumber">RESET</button>
            </div>
            </div>
            
            
        <!-- Text Conversion -->
        
        <h2>Text conversion</h2>
        
        <div class="box">

            <div class="textarea-group">
                <label >Enter your text below</label>
            
            <textarea name="text-field"  cols="30" rows="10"
             v-model="lines.text"
            
            ></textarea>
            </div>
            <div class="one-rem-space"></div>

        
        

        
        
            
            
            <div class="textarea-group">
                <label >Enter your Binary below</label>
            
            <textarea name="binary-field" id="" cols="30" rows="10"
             v-model="lines.binary"
            
            ></textarea>
            </div>
            <div class ="one-rem-mergin"></div>
            <div class="reset-btn-container">
        <button @click="resetLines">RESET</button>

            </div>
            </div>
            </section>
            </div>
            </div>
            </template>
            
        
    <script>
    require('@/assets/styles/reset.css');
    require('@/assets/styles/fonts.css');
    require('@/assets/styles/style.css');

    function isBinary(text){
        for(let t of text){
            if(t!=0 && t!=1) return false;
        }
        return true;
    }

    
    function isOctal(text){
        for(let t of text){
            if(t<0 || t>7) return false;
        }
        return true;
    }

    
    function isHex(text){
        for(let t of text){
            if(
            (t<0 || t>9)&&
            (t<'A'|| t>'F')&&
            (t<'a'||t>'f')
            ) {
            return false;
            }
        }
        return true;
    }

    function textToBinary(text){
        const charCodeArray = [];
        for(let i in text){
            charCodeArray.push(text.charCodeAt(i));
        }

        const binaryArray = charCodeArray.map((char)=>{
            return char.toString(2);
        });
        return binaryArray;
    }

    function binaryToText(codeArray) {
        let text = '';
        for(let code of codeArray) {
            const char = String.fromCharCode(parseInt(code,2));
            text = text.concat(char);
        }

        return text;
    }




    export default {
        name:'app',
        created() {
            document.title = 'Nano Conveter';
        },
         data(){
      return{
          numbers:{
              deciaml: 0,
              binary: 0,
              octal: 0,
              hexadecimal:0,
          },
         lines:{
               text:'',
              binary:'',
           },
           invalidNumber:false,
           invalidLine:false,
       };
  },
 methods: {
       resetNumber(){
           this.number={
               deciaml: 0,
               binary: 0,
               octal: 0,
             hexadecimal:0,
          };
          this.invalidNumber= false;
      },
  
  resetLines(){
          this.lines={
               text ='',
             binary:'',
             
          };
         this.invalidNumber= false;
  },
      },
  watch:{
     'numbers.deciaml': function(value){
          this.numbers.deciaml=purseInt(value) || 0;
          this.numbers.binary=value.toString(2);
          this.numbers.octal=value.toString(8);
          this.numbers.hexadecimal=value.toString(16);

      },
      'numbers.binary':function(value){
          let deciamal = parseInt(value,2)
          if(!isBinary(value)){
              this.invalidNumber=ture;
          }
          else{
              this.invalidNumber=false;
          }
          this.number.deciamal=deciamal;
          this.number.binary= value || 0;
          this.number.octal = deciamal.toString(8);
          this.number.hexadecimal = deciamal.toString(16);
          

      }, 
      'numbers.octal': function(value){
          let deciaml = parseInt(`0${value}`, 8)  || 0;
          if(!isOctal(value)){
              this.invalidNumber = true;
          } else{
              this.invalidNumber = false;
          }
          this.number.deciamal=deciamal;
          this.number.binary= deciaml.toString(2) || 0;
          this.number.octal = value || 0;
          this.number.hexadecimal = deciamal.toString(16);
          
      },
      'numbers.hexadecimal':function(value){
          let deciaml = parseInt(`0x${value}`, 16) || 0);
          if(!isHex(value)){
              this.invalidNumber = true;
          } else{
              this.invalidNumber = false;
          }
          this.number.deciamal=deciamal;
          this.number.binary= deciaml.toString(2) || 0;
          this.number.octal = deciaml.toString(8)
          this.number.hexadecimal = value || 0 ;

  },
  'lines.text': function (value){
      if(value.length==0){
          this.lines.binary ='';
      } else{
          const codeArray = textToBinary(value);
          this.line.binary = codeArray.join(' '); 
      }

  },
  'lines.binary': function(value){
      if(value.length==0){
          this.lines.text = ' ';
      } else{
          const codeArray = value.split(' ');
          const text = binaryToText(codeArray);
          this.lines.text = text;
      
      
  
}
},
 },
    };
    </script>
