<script lang="ts">
	import Icon from '@iconify/svelte';
	let totalIncome = 23000 + 0;
	let totalExpenses = 12194;
	let curAmount: number | string;

	$: balance = totalIncome - totalExpenses;

	function doTransaction(add: boolean): void {
		let betrag = 0;
		if (typeof curAmount === 'string') {
			betrag = parseInt(curAmount);
		} else {
			betrag = curAmount;
		}
		if (add) totalIncome += betrag;
		if (!add) totalExpenses += betrag;
		curAmount = 0;
	}

	function reset(): void {
		balance = 0;
		totalIncome = 0;
		totalExpenses = 0;
	}
</script>

<h1>Expense Tracks</h1>

<div class="display">
	<div class="totin">
		<h2>Total Income</h2>
		<p>$ {totalIncome}</p>
	</div>
	<div class="totexp">
		<h2>Total Expenses</h2>
		<p>$ {totalExpenses}</p>
	</div>
	<div class="totbalance">
		<h2>Total Balance</h2>
		<p>$ {balance}</p>
	</div>
</div>

<h1>New transaction</h1>

<div class="form">
	<div class="input">
		<input type="text" class="amount" bind:value={curAmount} placeholder="the amount" />
	</div>
	<div class="buttons">
		<button on:click={() => doTransaction(true)}><Icon icon="ic:baseline-plus" /></button>
		<button on:click={() => doTransaction(false)}><Icon icon="ic:baseline-minus" /></button>
	</div>
</div>
<div class="reset"><button on:click={reset}>Reset</button></div>

<div class="history">
	<p class="plus">$ 8000</p>
	<p class="minus">$ 4311</p>
</div>

<style lang="scss">
	@import './src/app.scss';

	h1 {
		text-align: center;
	}
	.totin,
	.totexp,
	.totbalance {
		@include datacard;
	}

	.form {
		/* kommt noch dran! */
		display: flex;
		justify-content: space-between;
		margin: 0 auto;
		max-width: 350px;

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

	.reset {
		margin-top: 1.5rem;
		text-align: center;
	}
</style>
