<template>
	<span class="app-text">
		<span
			v-show="isLoadded"
			ref="text"
		>
			<slot></slot>
		</span>
		<app-content-placeholder v-if="!isLoadded" :type="type" />
	</span>
</template>

<script lang="ts">
import { Vue, Component, Prop, Watch } from "vue-property-decorator";
// Components //
import AppContentPlaceholder from "@/components/app/content-placeholder.vue";

@Component({
	components: {
		AppContentPlaceholder
	}
})
export default class AppText extends Vue {
	@Prop({
		type: String,
		default: "line-single"
	}) type!: "word" | "line-single" | "line-multiple";

	isLoadded: boolean = false;
	checkText: number = -1;

	created() {
		this.checkText = setInterval(() => {
			if (this.$refs.text) {
				if ((this.$refs.text as Element).innerHTML.replace(/\s/g, "") != "") {
					this.isLoadded = true;
					clearInterval(this.checkText);
					this.checkText = -1;
				}
			} else {
				clearInterval(this.checkText);
				this.checkText = -1;
			}
		});
	}
	beforeDestroy() {
		if (this.checkText != -1) clearInterval(this.checkText);
	}
}
</script>
