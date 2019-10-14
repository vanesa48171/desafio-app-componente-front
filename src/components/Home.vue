<template>
  <div>
	<!--LISTADO DE EVENTOS-->
	<h1 class="proxEventos">Próximos Eventos</h1>
  <h4>EVENTO</h4>
	<div class="contenedorEventos"> <!-- contenedor de todos los eventos -->
		<div class="row">
      
			<div class="col-sm-6" v-for="evento in eventos" :key="evento.id">
        <br>
				<div class="card border-info">
					<div class="card-header border-info">
						<font style="vertical-align: heredar;">{{evento.fecha}}</font>
					</div>
					<div class="card-body">
						<h5 class="card-title">{{evento.nombre}}</h5>
						<!-- <p class="card-text"></p>  -->
						<router-link class="btn btn-celeste" :to="'/evento/'+ evento.idEvento">Ver Evento</router-link>
					</div>
				</div>
			</div>

		</div>
	</div>
  
</div>

</template>

<script>
export default {
  name: 'Home',
    data() {
    return {
       eventos: []     
    }
  },
  methods:{
    fetchData(){
      fetch('http://localhost:3000/eventos', {mode: 'cors'}).then((response)=>{
        return response.json();
      }).then((data)=> {
        this.eventos = data.map(item=>{
          item.fecha = new Date(item.fecha).toLocaleDateString()
          return item;
        })
        
        console.log('Request successful', data);
      }).catch((error)=>{
        console.log('Request failed', error)
      })
    }
  },
  mounted(){
    this.fetchData()
  }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url('https://fonts.googleapis.com/css?family=Modak&display');    
@import url('https://fonts.googleapis.com/css?family=Proza+Libre');
h1 {
    font-family: 'Mf Hey Pretty Girl';
    color: seagreen;
    font-weight: 300;
}
.proxEventos
{
	text-align: center;
	font-family: 'Mf Hey Pretty Girl';
	margin-top: 20px;
	font-size: 50px;
}

.btn-celeste
{
	/*background-color: #0CFBE4;*/
	background-color: #9dfbfb;
	color: black;
	margin-top: 20px;
	padding-right: 20px;
	width: 100px;
	font-size: 17px;
	letter-spacing: 0.5px;
}

.btn-celeste:hover{
  color: #FB8351;
}

/*h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.btn {
    display: inline-block;
    font-weight: normal;
    text-align: center;
    white-space: nowrap;
    vertical-align: middle;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    border: 1px solid transparent;
    padding: .375rem .75rem;
    line-height: 1.5;
    border-radius: .25rem;
    transition: color .15s ease-in-out, background-color .15s ease-in-out, border-color .15s ease-in-out, box-shadow .15s ease-in-out
}


.btn-celeste
{
	/*background-color: #0CFBE4;-
	background-color: #9dfbfb;
	color: black;
	margin-top: 20px;
	padding-right: 20px;
	width: 100px;
	font-size: 17px;
	letter-spacing: 0.5px;
}

.btn-celeste:hover{
  color: #FB8351;
}
*/
</style>
