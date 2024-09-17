<template>
	<div class="w-full md:w-1/2">
		<div class="leading-loose max-w-xl m-4 p-7 bg-secondary-light dark:bg-secondary-dark rounded-xl shadow-xl text-left">
			<p class="font-general-medium text-primary-dark dark:text-primary-light text-2xl mb-8">
				Contact Form
			</p>
			<form @submit.prevent="sendEmail" class="font-general-regular space-y-7" ref="contactForm">
				<FormInput label="Name" inputIdentifier="name" v-model="form.name" placeholder="Full Name"/>
				<FormInput label="Email" inputIdentifier="email" v-model="form.email" inputType="email" placeholder="Your Email"/>
				<FormInput label="Subject" inputIdentifier="subject" v-model="form.subject" />
				<FormTextarea label="Message" textareaIdentifier="message" v-model="form.message" placeholder="Write your message"/>

				<div>
					<Button
						title="Send Message"
						class="px-4 py-2.5 text-white tracking-wider bg-indigo-500 hover:bg-indigo-600 focus:ring-1 focus:ring-indigo-900 rounded-lg duration-500"
						type="submit"
						aria-label="Send Message"
					/>
				</div>
			</form>
		</div>
	</div>
</template>

<script>
import emailjs from 'emailjs-com';
import Button from '../reusable/Button.vue';
import FormInput from '../reusable/FormInput.vue';
import FormTextarea from '../reusable/FormTextarea.vue';

export default {
	components: { Button, FormInput, FormTextarea },
	data() {
		return {
			form: {
				name: '',
				email: '',
				subject: '',
				message: ''
			}
		};
	},
	methods: {
		sendEmail() {
			const serviceID = 'service_3glwmc9';
			const templateID = 'template_ih08m5z';
			const userID = 'iF0OKP-3UiGu_01Vz';

			const templateParams = {
				name: this.form.name,
				email: this.form.email,
				subject: this.form.subject,
				message: this.form.message
			};

			console.log('Sending email with parameters:', templateParams);

			emailjs.send(serviceID, templateID, templateParams, userID)
				.then(response => {
					console.log('Email sent successfully!', response.status, response.text);
					alert('Message sent successfully!');
					this.resetForm();
				})
				.catch(error => {
					console.error('Failed to send email.', error);
					alert('Failed to send message. Please try again later.');
				});
		},
		resetForm() {
			this.form.name = '';
			this.form.email = '';
			this.form.subject = '';
			this.form.message = '';
		}
	}
};
</script>

<style lang="scss" scoped></style>