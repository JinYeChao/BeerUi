<script lang='ts'>
	import '$lib/assets/scss/index.scss';
	import LayoutHeader from '$lib/demo/layout/LayoutHeader.svelte';
	import { page } from '$app/stores';
	import SideBar from '$lib/demo/layout/SideBar.svelte';
	import LayoutFooter from '$lib/demo/layout/LayoutFooter.svelte';

	$:formatUrl = () => {
		if ($page.url.pathname.indexOf('/svg') !== -1) {
			return '/' + $page.url.pathname.split('/')[1];
		}
		return $page.url.pathname;
	};
</script>
<div class='be-warp'>
	<LayoutHeader menu={formatUrl()} />
	<div class='be-container'>
		<SideBar />
		<div class='be-main'>
			<div class='be-main-container'>
				<slot></slot>
			</div>
			<LayoutFooter style='margin-left: 240px;background: #6b84ad;' />
		</div>
	</div>
</div>
<style lang='scss' global>
	.be-warp {
		height: 100%;
		overflow: hidden;
		background: var(--bg-color-container);
	}

	.be-main-container {min-height: calc(100vh - 60px);}
	.be-container, .be-main {
		height: calc(100vh - 60px);
		overflow-x: hidden;
		overflow-y: auto;
		position: relative;
		/* 设置滚动条的样式 */
		&::-webkit-scrollbar {
			width: 8px;
		}

		/* 滚动槽 */
		&::-webkit-scrollbar-track {
			-webkit-box-shadow: var(--scrollbar-color);
			border-radius: 6px;
		}

		/* 滚动条滑块 */
		&::-webkit-scrollbar-thumb {
			border-radius: 6px;
			background: rgba(0, 0, 0, 0.1);
			-webkit-box-shadow: var(--scrollbar-color);
		}
	}

	.page-container {
		margin-left: 260px;
		padding: 35px;

		h1, h2, h3, h4, h5, p {
			color: var(--text-color-primary)
		}
	}

	.demo-title {
		font-size: 22px;
		color: var(--text-color-primary);
		margin: 15px 0;
	}

	.demo-list {
		margin: 16px 0;
	}

	.demo-block {
		border: 1px solid var(--border-level-1-color);
		border-radius: 3px;
		transition: .2s;

		.source {
			padding: 24px;
		}

		.meta {
			background: var(--bg-color-code);
			border-top: 1px solid var(--border-level-2-color);
			transition: height .2s;
			overflow-y: hidden;
		}

		.description {
			padding: 20px;
			box-sizing: border-box;
			font-size: 14px;
			line-height: 22px;
			color: var(--text-color-primary);
			word-break: break-word;
			background-color: var(--bg-color-container);
		}

		table, tr, th, td {
			color: var(--text-color-primary);
		}

		&-control {
			border-top: solid 1px #eaeefb;
			height: 44px;
			box-sizing: border-box;
			background-color: #fff;
			border-bottom-left-radius: 4px;
			border-bottom-right-radius: 4px;
			display: flex;
			justify-content: center;
			align-items: center;
			text-align: center;
			margin-top: -1px;
			color: #d3dce6;
			cursor: pointer;
			position: relative;
			user-select: none;

			&.is-fixed {
				position: fixed;
				bottom: 0;
				width: 992px;
			}

			> span {
				font-size: 14px;
				line-height: 44px;
				transition: .3s;
				display: inline-block;
			}

			.triangle {
				margin-right: 10px;
				width: 0;
				height: 0;
				transition: .3s;
				transform-origin: center;
				border-left: 6px solid transparent;
				border-right: 6px solid transparent;
				border-bottom: 8px solid #d3dce6;

				&-down {
					transform: rotate(180deg);
				}
			}

			&:hover {
				color: #409EFF;
				background-color: #f9fafc;

				.triangle {
					border-color: transparent transparent #409EFF transparent;
				}
			}
		}
	}

	.demo-code-container {
		padding: 20px;
	}

	.pt-0 {
		padding-top: 0;
	}

	.pb-0 {
		padding-bottom: 0;
	}

	.high-code {
		width: 100%;
		background: var(--bg-color-code);
		border-radius: 6px;

		.hljs-tag {
			color: #878787;
		}

		code {
			background-color: transparent;
		}

		& * {
			margin: 0;
			padding: 0;
			border: 0;
			line-height: 2;
			font-family: Menlo, Monaco, Consolas, Courier, monospace;
			font-size: 12px;
		}
	}
</style>
