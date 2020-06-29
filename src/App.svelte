<script>
	$: mvtMaxValues = 1000000;
	$: mvtId = 500001;
	$: testOffset = 0.5;
	$: testAudience = 0.5;
	$: variants = ['v', 'v'];
	
	const isVariant = (i) =>  mvtId % variants.length === i;
	
	const isInTest = () => {
		const smallestTestId = mvtMaxValues * testOffset;
		const largestTestId = smallestTestId + mvtMaxValues * testAudience;

		return mvtId && mvtId > smallestTestId && mvtId <= largestTestId; 
	}
	
</script>

<h1>What's my variant?</h1>
<p>
	Add your MVT ID and the number of variants the A/B Test has to see which variant your MVT Id will fall into.
</p>

<h2>
	 AB Testing Framework Config
</h2>
<label>
	MVT Max Values
	<input type="number" bind:value={mvtMaxValues} />
</label>
<label>
	MVT ID
	<input type="number" bind:value={mvtId} />
</label>

<h2>
	AB Test Config
</h2>
<label>
	Test Audience ({testAudience * 100}%)
	<input type="number" step=".1" max="1" min={0}  bind:value={testAudience} />
</label>
<label>
		Test Offset ({testOffset * 100}%)
	<input type="number" step=".1" max="1" min={0} bind:value={testOffset} />
</label>

<div>
	<h2>
		Add/Remove Variants
	</h2>
	<button on:click={() => variants = [...variants, 'v']}>
		Add Variant
	</button>
	<button on:click={() => variants = variants.slice(0, variants.length - 1)}>
		Remove Variant
	</button>	
</div>

<h2 style="color: green;">
	Results
</h2>
<p>
	Variant will be highlighted.
</p>
<ul>
	<li>Is user in test? {mvtMaxValues,mvtId,variants,testAudience,testOffset, isInTest() ? 'Yes' : 'No'}</li>
	{#each variants as _, i}
		<li class={mvtMaxValues,mvtId,variants,testAudience,testOffset, isVariant(i) && isInTest() ?'highlight':''}>{i === 0?'Control':`Variant ${i}`} </li>
	{/each}
</ul>

<style>

	ul {
		list-style: none;	
		margin-left: 0;
		padding: 0;
	}
	
	li {
		border: 1px solid #444;
		margin-bottom: 10px;
		margin-right: 10px;
		padding: 10px;
		display: inline-block;
	}
	
	button {
		border: 1px solid #444;
		border-radius: 5px;
		background: #f6f6f6;
	}
	
	label {
		display: inline-block;
		margin-right: 10px;
	}
	
	input {
		padding: 10px;
	}
	
	.highlight {
		background-color: yellow;
	}
</style>