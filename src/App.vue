<template>
  <div id="led">

        <div id="led-position">  
            <div id="halfCircle" :class="classname"></div>
            <div id="rect" :class="classname"></div>
            <div id="bottom" :class="classname"></div>
            <div id="shine" :class="classname"></div>
            <div id="foot1" :class="classname"></div>
            <div id="foot2" :class="classname"></div>
        </div>

        <button @click="addKlick">switch</button>
        <p>{{ classname }}</p>  <!-- the getter lets me access it like a data prop of the component "Led" -->
        

  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      classname: 'red',
	  
    }	
  },
  //methods have to be outside of data()
  methods: {
        addKlick: () => {
		console.log(this.classname)
        this.classname = 'lightRed'
		console.log(this.classname)
        }
  	  }
 

  }



  const spacebroClient = require('spacebro-client')

spacebroClient.connect('spacebro.space', 3333, {
	clientName: 'Philipp',
	channelName: 'testChannel'
})


//subscribe to event 'connected'
spacebroClient.on('connected', function() { console.log('welcome')})
 

//subrsribe to event
spacebroClient.on('up', function() {
	console.log('up')
	io.sockets.emit('spaceUp')
})

spacebroClient.on('down', function() {
	console.log('down')
	io.sockets.emit('spaceDown')
})

//wait because node is async and needs time to connect
setTimeout(function(){
	spacebroClient.emit('connected')
}, 1000);


</script>

<style>

#led-position { 
	position: relative;
	margin: 70px auto;
	left: 70px;
	
}

#halfCircle {
	position: absolute;
	top: 0;
	height:50px;
    width:100px;
    border-radius: 100px 100px 0 0;
	
}

#rect {
	position: absolute;
	top: 50px;
	width: 100px;
	height: 100px;
	
}

#bottom {
	position: absolute;
	top: 150px;
	width: 110px;
	height: 15px;
	
}

#shine {
	position: absolute;
	left: 63px;
	top: 15px;
	width: 30px;
	height: 15px;
	border-radius: 100%;
	background: rgba(255,255,255,0.5);
	transform: rotate(45deg);
}

#foot1 {
	position: absolute;
	left: 25px;
	top: 165px;
	width: 5px;
	height: 180px;
	background: rgba(100,100,100,0.5);
}

#foot2 {
	position: absolute;
	left: 75px;
	top: 165px;
	width: 5px;
	height: 230px;
	background: rgba(100,100,100,0.5);
}

body {
	font-family: sans-serif;
}



.red {
	background: red;
}

.lightRed {
	background: rgba(255,0,0,0.5);
}
</style>
