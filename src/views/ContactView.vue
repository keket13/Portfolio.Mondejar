<script setup>
import MainLayout from '../components/MainLayout.vue';

// Page Title of Views
const pageTitle = 'Contact'
</script>

<template>
  <MainLayout :pageTitle="pageTitle">
    <section>
      <div class="company-info">
       <div class="head">
			<h3>Contact us</h3>
    </div> 

			<ul>
				<li><i class="fa fa-road"></i>Ibabao Basak Lapu-Lapu City, Cebu 6015</li>
				<li><i class="fa fa-phone"></i>09298019939</li>
				<li><i class="fa fa-envelope"></i>keketh13@gmail.com</li>
			</ul>
		</div>
		<!-- End .company-info -->

		<!-- CONTACT FORM -->
		<div class="contact">
      <div class="heads">
			  <h3>Need to reach out? Fill out the form.</h3>
      </div>

			<form id="contact-form">

				<p>
					<label>Name</label>
					<input type="text" name="name" id="name" required>
				</p>

				<p>
					<label>E-mail Address</label>
					<input type="email" name="email" id="email" required>
				</p>

				<p class="full">
					<label>Message</label>
					<textarea name="message" rows="5" id="message"></textarea>
				</p>

				<p class="full">
					<button type="submit">Submit</button>
				</p>

			</form>
			<!-- End #contact-form -->
		</div>
    </section>
  </MainLayout>
</template>

<style>
@import url('https://fonts.googleapis.com/css?family=Yantramanav:100,300');

* {
  box-sizing: border-box;
}

body {
  line-height: 1.6;
  font-family: 'Yantramanav', sans-serif;
  padding: 1em;
}

.container {
  max-width: 1170px;
  margin-left: auto;
  margin-right: auto;
  padding: 1em;
}
.head{
  font-weight: 600;
  font-size: 40px;
}
.heads{
  font-weight: 650;
  word-spacing: 5px;
  margin-bottom: 30px;
  text-align: center;
}

ul {
  list-style: none;
  padding: 0;
  font-weight: 600;
}

.brand {
  text-align: center;
	font-weight: 300;
	text-transform: uppercase;
	letter-spacing: 0.1em;
}

.brand span {
  color: #ffffff;
}

.wrapper {
  box-shadow: 0 0 20px 0 rgba(57, 82, 163, 0.7);
}

.wrapper > * {
  padding: 1em;
}
label{
  font-weight: 600;
}

.company-info {
  background: #ffffff;
  border-top-left-radius: 4px;
  border-top-right-radius: 4px;
}

.company-info h3,
.company-info ul {
  text-align: center;
  margin: 0 0 1rem 0;
}

.contact {
  background: #ffffff;
  border-bottom-left-radius: 4px;
  border-bottom-right-radius: 4px;
}

.contact form {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 20px;
}

.contact form label {
  display: block;
}

.contact form p {
  margin: 0;
}

.contact form .full {
  grid-column: 1 / 3;
}

.contact form button,
.contact form input,
.contact form textarea {
  width: 100%;
  padding: 1em;
  border: solid 1px #fabc86;
  border-radius: 4px;
}

.contact form textarea {
  resize: none;
}

.contact form button {
  background: #ffe4b2;
  border: 0;
  color: #000000;
  text-transform: uppercase;
  font-size: 14px;
  font-weight: bold;
}

.contact form button:hover,
.contact form button:focus {
  background: #ff9500;
  color: #ffffff;
  outline: 0;
  transition: background-color 2s ease-out;
}

@media only screen and (min-width: 700px) {
  .wrapper {
    display: grid;
    grid-template-columns: 1fr 2fr;
  }

  .wrapper > * {
    padding: 2em;
  }

  .company-info {
    border-radius: 4px 0 0 4px;
  }

  .contact {
    border-radius: 0 4px 4px 0;
  }

  .company-info h3,
  .company-info ul,
  .brand {
    text-align: left;
  }
}
</style>