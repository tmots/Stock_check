<script>
	let array = [0]
	let buy = [];
	let sale = [];
	let comm = [0.07];
	let quan = [20];

	function add_fnc(){
		array = [...array, array.length + 1];
	}
	function Close_fnc(){
		array = array.splice(1)
	}

	let lin = "amd"

	function naverlink_fnc(urlm){
		window.open('https://m.stock.naver.com/worldstock/stock/'+urlm+'.O/price');
	}
	function mwlink_fnc(urlm){
		window.open('https://www.marketwatch.com/investing/stock/'+urlm+'/charts?mod=mw_quote_advanced');
	}
</script>

<div class="title_div">수익계산기</div>
<div class="chartdiv">
<input type=string bind:value={lin}><br>
<button on:click={naverlink_fnc(lin.toUpperCase())}>Naver</button><button on:click={mwlink_fnc(lin.toLowerCase())}>MarketWatch</button>
</div>
<div class="add_btn">
	<button on:click={add_fnc}>Add</button> / <button on:click={Close_fnc}>Close</button><br>
</div>

{#each array as data, index}
	<div class="mainBox">
		<label>
			매 수 가 : <input type=number bind:value={buy[index]} min=0 max=9999> $<br>
			매 도 가 : <input type=number bind:value={sale[index]} min=0 max=9999> $<br>
			수 수 료 : <input type=number bind:value={comm[index]} min=0 max=9999> %<br>
			거 래 량 : <input type=number bind:value={quan[index]} min=0 max=9999> 개<br>
		</label>
		<div class="bene">
			<p>수익금 : {(sale[index] * quan[index] - buy[index] * quan[index])-(sale[index] * quan[index] * (comm[index] / 100) + buy[index] * quan[index] * (comm[index] / 100)).toFixed(2)}</p>
		</div>
	</div>
{/each}