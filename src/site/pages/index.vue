<template>
	<div>
		<div class="logoContainer">
			<Logo />
		</div>
		<div class="leftSpacer">
			<div class="mainBlock">
				<div>
					<h4>Fuego Creators - Image Hosting</h4>
					<p>
						Welcome to the public CDN for Fuego Creators.<br>This site is open to anyone to host their art, portfolios, images, uploads, or anything else you need.<br>If you have any questions, email us at admin@fuegocreators.com
					</p>
					<div class="mt4" />
					<Uploader v-if="config.publicMode || (!config.publicMode && loggedIn)" />
					<div
						v-else
						class="has-text-right is-size-4">
						This site has disabled public uploads. You need an account.
					</div>

					<Links />
				</div>
			</div>
		</div>
	</div>
</template>
<script>
import { mapState, mapGetters } from 'vuex';

import Logo from '~/components/logo/Logo.vue';
import Uploader from '~/components/uploader/Uploader.vue';
import Links from '~/components/home/links/Links.vue';

export default {
	name: 'Home',
	components: {
		Logo,
		Uploader,
		Links
	},
	data() {
		return { albums: [] };
	},
	computed: {
		...mapGetters({ loggedIn: 'auth/isLoggedIn' }),
		...mapState(['config'])
	},
	head() {
		return {
			title: 'Home'
		};
	}
};
</script>
<style lang="scss" scoped>
	.logoContainer {
		position: fixed;
		top: calc(45% - 188px);
		left: calc(22% - 117px);
	}
	.leftSpacer {
		width: 56%;
		margin-left: auto;
		position: relative;
		.mainBlock {
			height: calc(100vh - 52px);
			position: relative;
			margin: 0 5rem;
			text-align: right;
			> div {
				position: absolute;
				top: 25%;
			}
		}
		p {
			font-size: 1.25em;
			margin-top: 1rem;
		}
		strong {
			text-decoration: underline;
		}
	}

	@media (max-width: 1025px) {
		.logoContainer {
			position: relative;
			top: 0;
			left: 0;
			text-align: center;
		}
		.leftSpacer {
			width: 100%;
			.mainBlock {
				height: auto;
				padding: 2rem 0;
				> div {
					top: 0rem;
					position: relative;
					text-align: center;
				}
			}
		}
	}
</style>
