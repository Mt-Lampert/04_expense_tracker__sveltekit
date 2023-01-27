<script lang="ts">
	import Icon from '@iconify/svelte';
</script>

<h1>Expense Tracks</h1>

<div class="display">
	<div class="totin">
		<h2>Total Income</h2>
		<p>$ 23000</p>
	</div>
	<div class="totexp">
		<h2>Total Expenses</h2>
		<p>$ 12394</p>
	</div>
	<div class="totbalance">
		<h2>Total Balance</h2>
		<p>$ 12394</p>
	</div>
</div>

<h1>New transaction</h1>

<div class="form">
	<div class="input">
		<input type="text" class="amount" placeholder="the amount" />
	</div>
	<div class="buttons">
		<button><Icon icon="ic:baseline-plus" /></button>
		<button><Icon icon="ic:baseline-minus" /></button>
	</div>
</div>

<div class="history">
	<p class="plus">$ 8000</p>
	<p class="minus">$ 4311</p>
</div>

<style lang="scss">
	@import './src/app.scss';

	.form {
		/* kommt noch dran! */
		display: flex;
		gap: 0.5rem;
		margin: 0 1rem;

		.amount {
			padding: 10px 9px;
			border-radius: 8px;
		}

		.buttons {
			display: flex;
			flex-direction: column;
		}
	}

	.amount {
		font-size: 1.25rem;
		border-radius: 5px;
	}

	.buttons {
		> button {
			display: inline-block;
		}
	}
</style>
