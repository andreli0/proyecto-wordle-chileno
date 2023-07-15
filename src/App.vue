<template>
  <nav class="navbar navbar-expand-lg bg-body-tertiary" style="height: 4.4vh;">
  <div class="container-fluid justify-content-center">
      <h3 class="mt-2">WORDLE</h3>
  </div>
</nav>
  <div class="container-fluid" style="height: 95.6vh;">
    
      <div class="d-flex align-items-center justify-content-center h-100 " v-on:keyup="addLetra">
          <table class="tabla" v-on:key="checkFocus">
              <tr class="fila" v-for="(row, index) in cuadros" :key="index">
                <td class="columna" v-for="(col,index) in row" :key="index">{{ col.value }}</td>
              </tr>
          </table>
      </div>
    </div>
</template>

<style scoped>
  .container-fluid{
    background-color: #6D5D6E !important;
  }
  .tabla{
    border-collapse: separate;
    border-spacing:1vh 1vh;
  }
  .columna{
    background-color: #393646;
    border:2px solid;
    border-color: #F4EEE0;
    height: 7vh;
    width: 7vh;
    color: #F4EEE0;
    font-size: 4vh;
    text-align: center;
  }
</style>

<script>
//import Title from './components/HelloWorld.vue'
export default {
  name: 'App',
  data: function(){
    return {
      cuadros: {
        row1: {
          col1:{'value':'','state':'focus'},
          col2:{'value':'','state':'void'},
          col3:{'value':'','state':'void'},
          col4:{'value':'','state':'void'},
          col5:{'value':'','state':'void'}
        },
        row2: {
          col1:{'value':'','state':'void'},
          col2:{'value':'','state':'void'},
          col3:{'value':'','state':'void'},
          col4:{'value':'','state':'void'},
          col5:{'value':'','state':'void'},
        },
        row3: {
          col1:{'value':'','state':'void'},
          col2:{'value':'','state':'void'},
          col3:{'value':'','state':'void'},
          col4:{'value':'','state':'void'},
          col5:{'value':'','state':'void'},
        },
        row4: {
          col1:{'value':'','state':'void'},
          col2:{'value':'','state':'void'},
          col3:{'value':'','state':'void'},
          col4:{'value':'','state':'void'},
          col5:{'value':'','state':'void'},
        },
        row5: {
          col1:{'value':'','state':'void'},
          col2:{'value':'','state':'void'},
          col3:{'value':'','state':'void'},
          col4:{'value':'','state':'void'},
          col5:{'value':'','state':'void'},
        },
        row6: {
          col1:{'value':'','state':'void'},
          col2:{'value':'','state':'void'},
          col3:{'value':'','state':'void'},
          col4:{'value':'','state':'void'},
          col5:{'value':'','state':'void'},
        }


      },
      intentos: {
        1:"",
        2:"",
        3:"",
        4:"",
        5:"",
        6:""
      }
    }
  },
  created(){
    
    window.addEventListener('keydown', (e) => {
      if ((e.key).match(/[a-z]/i) && (e.key).length == 1) {
        this.escribir(e.key);
        this.checkFocus();
      }else if(e.key == "Backspace"){
        this.borrar();
      }
    });
  },
  methods: {
    checkFocus(){
      let skip = false
      Object.values(this.cuadros).forEach(y=>{
        Object.values(y).forEach(x=>{
          if(skip){
            return;
          }
          if(x.value==""){
            skip = true;
            return x.state = "focus";
          }
        })
      })
    },
    escribir(key){
      let skip = false;
      Object.values(this.cuadros).forEach(y=>{
        Object.values(y).forEach(x=>{
          if(skip){
            return;
          }
          if(x.state=="focus"){
            skip = true;
            x.state = "hasvalue"
            return x.value = key;
          }
        })
      })
    },
    borrar(){
      let skip = false;
      for(let y = 6; y >= 1 ;y--){
        for(let x = 5; x >= 1 ;x--){
          let col = this.cuadros["row"+y]["col"+x];
          if(skip){
            return;
          }
          if(col.state == "focus" && x > 1){
            this.cuadros["row"+y]["col"+x].value = "";
            this.cuadros["row"+y]["col"+x].state = "void";
            this.cuadros["row"+y]["col"+(x-1)].value = "";
            this.cuadros["row"+y]["col"+(x-1)].state = "focus";
            return;
          }
        }
      }
    }

  }

}
</script>



