<template>
  <section class="home">
  	<!-- animation -->
  	<jack-anm :show="platformPopUp"></jack-anm>
    <!-- popUp -->
    <jack-popUp v-if="platformPopUp" @popUpClose="popUpClose">
    	<p class="pop-content">{{msg}}</p>
    </jack-popUp>
  </section>
</template>

<script>
import popUp from "@/components/common/popUp"
import anm from "@/components/common/anm"

export default {
  name: 'home',
  data () {
    return {
    	msg: "You're not a platform for mobile phones.",
    	platformPopUp: false
    }
  },
  mounted() {
	  	this.$nextTick(()=>{
				if(navigator.platform.indexOf("Win")!=-1 || navigator.platform.indexOf("Mac")!=-1){
					this.platformPopUp = sessionStorage.getItem("platformPopUp") ? false : true;
				};
	  	})
	},
  components: {
  	"jack-popUp": popUp,
  	"jack-anm": anm
  },
  methods: {
  	popUpClose() {
  		this.platformPopUp = false;
  		sessionStorage.setItem("platformPopUp","done");
  	}
  }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	.pop-content{
		font: bold 1.3rem/2.2rem "arial, helvetica, sans-serif";
		color: orange;
		width: 21rem;
		border-radius: 1rem;
    background: white;
		padding: 2.5rem 1.5rem 2rem;
	}
</style>
