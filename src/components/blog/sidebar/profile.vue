<template>
	<div class="blog-sidebar-profile">
		<app-profile-image
			:src="$store.state.blog.owner.profileImage"
			class="profile-image"
		/>
		<div class="name">
			<app-text type="word" class="nick">
				{{ $store.state.blog.owner.nickname }}
			</app-text>
			<app-text type="word" class="real">
				{{ $store.state.blog.owner.realname }}
			</app-text>
		</div>
		<app-text type="line-multiple" class="desc">
			{{ $store.state.blog.description }}
		</app-text>
		<app-button-tag
			v-if="$store.getters.isAdmin"
			type="route"
			:to="{ name: 'AdminBasic' }"
			class="edit-profile"
		>
			<i class="material-icons icon">edit</i>
			<template #tag>프로필 편집</template>
		</app-button-tag>
	</div>
</template>

<script lang="ts">
import { Vue, Component } from "vue-property-decorator";
// Components //
import AppProfileImage from "@/components/app/image-profile.vue";
import AppText from "@/components/app/text.vue";
import AppButtonTag from "@/components/app/button-tag.vue";

@Component({
	components: {
		AppProfileImage,
		AppText,
		AppButtonTag
	}
})
export default class BlogSidebarProfile extends Vue {}
</script>

<style lang="scss" scoped>
@import "../../../assets/styles/variables";

$profile-image-size: $sidebar-width - $sidebar-padding * 2;

.blog-sidebar-profile {
	position: relative;
}

.profile-image {
	display: block;

	width: $profile-image-size;
	height: $profile-image-size;
	margin-bottom: 16px;
	border-radius: 100%;

	background-color: $background-color-lv2;

	.image {
		width: 100%;
		height: 100%;

		border-radius: 100%;
	}
}
.name {
	display: flex;

	margin-bottom: 8px;

	flex-direction: column;

	.nick {
		font: {
			size: xx-large;
			weight: bold;
		}

		line-height: 1em;
	}
	.real {
		color: $text-color-white-disable;
		font: {
			size: large;
			weight: 100;
		}
	}
}
.desc {
	color: $text-color-white-desc;
	font-size: 14px;
}
.edit-profile {
	position: absolute;
	top: calc(#{$profile-image-size} - 48px);
	right: 0;

	width: 48px;
	height: 48px;

	border: 4px solid $background-color-lv1;
	border-radius: 100%;

	background-color: $background-color-lv2;

	transition: background-color 0.1s;

	&:hover {
		background-color: $background-color-lv3;
	}
}
</style>
