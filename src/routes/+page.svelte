<script lang="ts">
	interface Zone {
		name: string;
		lowerBound: number;
		upperBound: number;
	}
	let zones: Zone[] = [
		{ name: '1', lowerBound: 0.5, upperBound: 0.6 },
		{ name: '2', lowerBound: 0.6, upperBound: 0.7 },
		{ name: '3', lowerBound: 0.7, upperBound: 0.8 },
		{ name: '4', lowerBound: 0.8, upperBound: 0.9 },
		{ name: '5', lowerBound: 0.9, upperBound: 1 }
	];

	let age = 18;

	let maxHeartRate = 220 - age;
</script>

<section class="m-5">
	<h1 class="text-3xl mb-5">Heartrate Zone Calculator</h1>
	<div class="bg-slate-800 inline-block p-3 shadow-sm">
		<div class="inline-grid grid-cols-[auto_auto] gap-3">
			<label for="age">Age</label>
			<input
				type="number"
				max="100"
				id="age"
				class="bg-slate-700 rounded px-2 py-1 hover:bg-slate-600 transition"
				value={age}
				on:input={(e) => {
					maxHeartRate = 220 - e.currentTarget.valueAsNumber;
					age = e.currentTarget.valueAsNumber;
				}}
			/>
			<label for="mhr"> Max Heart Rate </label>
			<input
				type="number"
				id="mhr"
				class="bg-slate-700 rounded px-2 py-1 hover:bg-slate-600 transition"
				value={maxHeartRate}
				on:input={(e) => {
					age = 220 - e.currentTarget.valueAsNumber;
					maxHeartRate = e.currentTarget.valueAsNumber;
				}}
			/>
		</div>
		<p class="italic text-sm text-slate-400 mt-3">Max Heart Rate = 220 - Age</p>
	</div>
	<table class="table-auto bg-slate-800 mt-2 p-3">
		<thead class="text-left bg-sky-900">
			<th class="p-2">Zone</th>
			<th class="p-2">Intensity (%)</th>
			<th class="p-2">Heart Rate (BPM)</th>
		</thead>
		<tbody>
			{#each zones as zone, i}
				<tr class="">
					<td class="p-2">{zone.name}</td>
					<td class="p-2"
						><input
							value={zone.lowerBound * 100}
							type="number"
							on:input={(e) => (zones[i].lowerBound = e.currentTarget.valueAsNumber / 100)}
							class="bg-slate-700 w-14 rounded px-2 py-1 hover:bg-slate-600 transition"
						/>% to
						<input
							type="number"
							value={zone.upperBound * 100}
							class="bg-slate-700 w-14 rounded px-2 py-1 hover:bg-slate-600 transition"
							on:input={(e) => (zones[i].upperBound = e.currentTarget.valueAsNumber / 100)}
						/>%</td
					>
					<td class="p-2">
						{(zone.lowerBound * maxHeartRate).toFixed(0)}
						- {(zone.upperBound * maxHeartRate).toFixed(0)}
					</td>
				</tr>
			{/each}
		</tbody>
	</table>
</section>
