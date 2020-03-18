<template lang="html">

	<section class="lightbox">
		<div class="main">
			<div class="row">
				<div class="column" v-for="image in images">
					<img :src="image.source" :alt="image.alttext" class="hover-shadow cursor"/>
				</div>
			</div>
			<div id="lightbox" class="modal">
				<span class="close cursor">&times;</span>
				<div class="modal-content">
					<div class="mySlides" v-for="image in images">
						<img :src="image.source" :alt="image.alttext"/>
					</div>
					<a class="prev">&#10094;</a>
					<a class="next">&#10095;</a>
				</div>
			</div>
			</div>
	</section>

</template>

<script lang="js">

	export default {
		name: 'lightbox',
		props: {
      images: {
        type: Array
      }
    },
		mounted () {
			this.initLightbox();
		},
		data () {
			return {

			}
		},
		methods: {
			initLightbox: function(){
				var body = document.getElementsByTagName("body")[0];

				var defaultIndex = 1;

				function showSlides(n) {

					var i;
					var slides = document.getElementsByClassName("mySlides");

					if (n > slides.length) {

						defaultIndex = 1;

					}

					if (n < 1) {

						defaultIndex = slides.length;

					}

					for (i = 0; i < slides.length; i++) {

						slides[i].style.display = "none";

					}

					slides[defaultIndex-1].style.display = "block";

				}

				showSlides(defaultIndex);

				function openModal(n) {

					document.getElementById("lightbox").style.display = "block";
					body.style.position = "fixed";

					showSlides(defaultIndex = n);

				}

				var col = document.getElementsByClassName("column");
				var i = 0;

				for(i; i < col.length; i++){

					col[i].children[0].onclick = (function(i){

						return function(){

							openModal(i+1);
							console.log(i);

						}

					})(i);

				}

				var prev = document.getElementsByClassName("prev")[0];
				var next = document.getElementsByClassName("next")[0];
				var close = document.getElementsByClassName("close")[0];

				prev.addEventListener("click", function(){

					showSlides(defaultIndex -= 1);

				});

				next.addEventListener("click", function(){

					showSlides(defaultIndex += 1);

				});

				close.addEventListener("click", function(){

					document.getElementById("lightbox").style.display = "none";
					body.style.position = "";

				});

				var dw = document || window;

				dw.onclick = function (event) {

					var modal = document.getElementById("lightbox");

					if (event.target == modal) {

						modal.style.display = "none";
						body.style.position = "";

					}

				}
			}
		},
		computed: {

		}
}


</script>

<style scoped lang="scss">
.lightbox {

}

.row > .column {
	padding: 0 8px;
}

.row:after {
	content: "";
	display: table;
	clear: both;
}

.column {
	float: left;
	width: 100%;
	margin-bottom: 10px;
}

.modal {
	display: none;
	position: fixed;
	z-index: 1;
	left: 0;
	top: 0;
	width: 100%;
	height: 100%;
	overflow: auto;
	background-color: black;
}

.modal-content {
	position: relative;
	background-color: #fefefe;
	margin: auto;
	padding: 0;
	width: 80%;
	height: auto;
	top: 30%;
	transform: translateY(-100px);
}

.close {
	color: white;
	position: absolute;
	top: 10px;
	right: 25px;
	font-size: 35px;
	font-weight: bold;
}

.close:hover,
.close:focus {
	color: #999;
	text-decoration: none;
	cursor: pointer;
}

.mySlides {
	display: none;
}

.prev,
.next {
	cursor: pointer;
	position: absolute;
	top: 50%;
	width: auto;
	padding: 16px;
	margin-top: -25px;
	color: white;
	font-weight: bold;
	font-size: 20px;
	transition: 0.6s ease;
	border-radius: 0 3px 3px 0;
	user-select: none;
	-webkit-user-select: none;
}

.prev {
	left: 0;
}

.next {
	right: 0;
	border-radius: 3px 0 0 3px;
}

.prev:hover,
.next:hover {
	background-color: rgba(0, 0, 0, 0.8);
}

img {
	margin-bottom: -4px;
	width: 100%;
}

img.hover-shadow {
	transition: 0.3s;
}

.hover-shadow:hover {
	box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}
</style>
