<script lang="ts">
	import Icon from '@iconify/svelte';

	type transaction = {
		amount: number;
		timestamp: string;
	};

	let totalIncome = 23000 + 0;
	let totalExpenses = 12194;
	let curAmount: number | string;
	let transactions: transaction[] = [];
	let theInput: any;

	$: balance = totalIncome - totalExpenses;

	function doTransaction(add: boolean): void {
		let betrag = 0;
		if (typeof curAmount === 'string') {
			betrag = parseInt(curAmount);
		} else {
			betrag = curAmount;
		}
		if (add) {
			totalIncome += betrag;
		}
		if (!add) {
			totalExpenses += betrag;
			betrag = betrag - 2 * betrag;
		}

		transactions = [{ amount: betrag, timestamp: formatNow() }, ...transactions];
		theInput.value = '';
		theInput.focus();
	}

	function formatNow(): string {
		const now = new Date(Date.now());
		const output =
			now.getFullYear() +
			'-' +
			now.getMonth() +
			1 +
			'-' +
			(now.getDate() < 10 ? '0' : '') +
			now.getDate() +
			' ' +
			now.getHours() +
			':' +
			now.getMinutes() +
			':' +
			now.getSeconds();
		return output;
	}

	function reset(): void {
		balance = 0;
		totalIncome = 0;
		totalExpenses = 0;
		transactions = [];
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
		<input
			bind:this={theInput}
			bind:value={curAmount}
			class="amount"
			placeholder="the amount"
			type="text"
		/>
	</div>
	<div class="buttons">
		<button on:click={() => doTransaction(true)}><Icon icon="ic:baseline-plus" /></button>
		<button on:click={() => doTransaction(false)}><Icon icon="ic:baseline-minus" /></button>
	</div>
</div>
<div class="reset"><button on:click={reset}>Reset</button></div>

<div class="history">
	{#each transactions as trs (trs.timestamp)}
		<p><span class={trs.amount >= 0 ? 'green' : 'red'}>{trs.amount}</span> ({trs.timestamp})</p>
	{:else}
		<p />
	{/each}
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

	.history > p {
		text-align: center;
	}
	.green {
		color: hsl(106, 97%, 27%);
	}

	.red {
		color: hsl(0, 97%, 47%);
	}
</style>
