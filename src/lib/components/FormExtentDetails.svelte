<script lang="ts">
	import { P } from 'flowbite-svelte';
	import PositiveNumberInput from './PositiveNumberInput.svelte';

	import { data } from '$lib/store/store';

</script>

<div class="flex gap-4 flex-col">
<P>
In a first step, we need to be able to convert credit points from <i>your credit point system</i> (as listed in your transcript) <i>to ECTS credit points</i> (our system). <span class="font-bold">Do not convert credit points from your system to ECTS yourself, we will do that from the information you provide here.</span> If your transcript contains credit points in two different systems, like ECTS and a system local to your country or university, please stick to <b>one</b> of these systems throughout the entire form and provide consistent answers. Also, <b>never enter grade point averages or marks.</b>
</P>
<P>
So now we need two pieces of information from you:
</P>
<ul class="list-disc space-y-6 pl-6">
	<li>
		<div class="grid grid-cols-[1fr_auto] gap-x-8 items-start">
			<P>
				The <b>standard</b> period of study in your bachelor program in months
				(<b>not the time you needed to finish your individual study</b>).
				This value should typically be between 36 and 60.
			</P>

			<div class="flex flex-col items-center">
				<PositiveNumberInput
					bind:value={$data["extentDetails"]["duration"]}
					class="w-24 text-center"
				/>
				<span class="mt-1 text-xs text-gray-500">months</span>
			</div>
		</div>
	</li>

	<li>
		<div class="grid grid-cols-[1fr_auto] gap-x-8 items-start">
			<P>
				The total number of credit points <b>that have to</b> be earned in your
				bachelor program (<b>not the credit points you earned, which might be more</b>).
			</P>

			<div class="flex flex-col items-center">
				<PositiveNumberInput
					bind:value={$data["extentDetails"]["points"]}
					class="w-24 text-center"
				/>
				<span class="mt-1 text-xs text-gray-500">credits</span>
			</div>
		</div>
	</li>
</ul>

{#if $data["extentDetails"]["duration"] != null && $data["extentDetails"]["points"] != null}
	{@const ratio =
		($data["extentDetails"]["duration"] / $data["extentDetails"]["points"]) * 5}

	{#if ratio < 0.7 || ratio > 2.5}
<div class="mt-4 rounded-lg border border-red-300 bg-red-50 p-4 text-sm text-red-900">
	<div class="flex items-start gap-2">
		<span class="text-red-700 text-lg">⚠️</span>
		<div>
			<p class="font-semibold">Please verify your entries.</p>
			<p>
				The entered duration and credits result in an unusual ratio
				({ratio.toFixed(2)} months per 5 credits). Please double-check that you
				have entered the <b>standard duration</b> of your bachelor's program
				and the <b>total number of credits required for graduation</b>.
			</p>
		</div>
	</div>
</div>
	{/if}
{/if}

</div>
