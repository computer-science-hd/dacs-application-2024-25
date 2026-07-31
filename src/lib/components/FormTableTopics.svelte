<script lang="ts">
import {
	Button,
	Checkbox,
	Heading,
	Input,
	P,
	Select,
	Table,
	TableBody,
	TableBodyCell,
	TableBodyRow,
	TableHead,
	TableHeadCell,
	type SelectOptionType
} from 'flowbite-svelte';
import { TrashBinOutline }  from 'flowbite-svelte-icons';

import PositiveNumberInput from './PositiveNumberInput.svelte';
import GenericValidatedInput from './GenericValidatedInput.svelte';
import { formTopics } from '$lib/topics';

import { data, addLecture, deleteLecture, addSkill, checkDuplicateLecture } from '$lib/store/store';

import { formSubjectAreas } from '$lib/subjectAreas';

const subjectSelectionItems: Array<SelectOptionType<Subject>> =
	formSubjectAreas.map((subjectArea) => ({
		value: subjectArea.subject,
		name: subjectArea.subject
	}));

</script>

<P>
Declare the lectures that provide the following <b>basic</b> skills. The skills are organized into seven basic topics ("Practical computer science", ...) in the subject area of computer science, followed by two topics ("Linear algebra", "Calculus") in the subject area of mathematics. A lecture may contribute to multiple topics within its subject area, which is why lectures are <b>replicated on purpose</b> across the topics within a subject area. 
</P>
<br>
<P>
For each lecture, provide its name as listed in your transcript (translated to English), the credit points (in <b>your credit point system</b>, as described above, i.e., no grade point averages, marks etc.), declare the <b>basic</b> skills it provides by checking the respective checkboxes (do <b>not</b> declare skills that are not specifically provided by the lecture), enter its official module description (as, e.g., provided in the module handbook of your field of study, translated to English if applicable), and declare if the lecture belongs to computer science or mathematics. Be aware that your list of lectures and skill selection will be checked by the admission commission, and for skill assessment only those lectures will be taken into account where a basic skill has been obtained, not where it has been applied. For example, a lecture "Artificial Intelligence" that applies linear algebra cannot be accredited for a basic linear algebra skill.
</P>
<br>
<P>
However, you are <b>encouraged</b> to add relevant computer science or mathematics lectures without selecting a topic. These lectures will be included in the subject-area assignment but will not be counted as evidence for a specific basic skill.
</P>
<br>
<P>
When assigning credits to skills according to this form, the credits of a lecture may be distributed across several skills. In the subsequent calculations, each lecture contributes at most in total its actual number of credits, and there is an upper bound for the number of credits per skill. 
</P>
{#each formTopics as topic}
<div class="my-4">
	<Heading tag="h4" class="mb-4">{topic.name}</Heading>
	<!--<Table class="overflow-x-auto" striped={true}>	-->
	<div class="overflow-x-auto w-full">
	<!--<Table striped={true} class="min-w-max">-->
	<Table striped={true} class="overflow-x-auto">
			<TableHead class="normal-case bg-primary-700 text-white">
				<!--<TableHeadCell class="min-w-60 text-2xs p-2">Lecture Name in Transcript</TableHeadCell>-->
				<TableHeadCell class="min-w-60 text-2xs p-2 text-center align-middle">Lecture Name in Transcript</TableHeadCell>
				<!--<TableHeadCell class="w-12 text-2xs p-2">Points</TableHeadCell>-->
				<TableHeadCell class="w-12 text-2xs p-2 text-center align-middle">Points</TableHeadCell>
				{#each topic.subtopics as subTopic}
					<!--<TableHeadCell class="text-2xs p-2 m-auto">{subTopic}</TableHeadCell>-->
					<TableHeadCell class="text-2xs p-2 text-center align-middle">{subTopic}</TableHeadCell>
				{/each}
				<!--<TableHeadCell class="text-2xs p-2">Module Description</TableHeadCell>-->
				<!--<TableHeadCell class="text-2xs p-2 text-center align-middle">Module Description</TableHeadCell>
				<TableHeadCell class="text-2xs p-2"></TableHeadCell>-->
				<TableHeadCell class="text-2xs p-2 text-center align-middle">Module Description	</TableHeadCell>
				<TableHeadCell class="min-w-40 text-2xs p-2 text-center align-middle">Subject Area</TableHeadCell>
				<TableHeadCell class="text-2xs p-2"></TableHeadCell>
			</TableHead>
			<TableBody>
				{#each $data.lectures as lecture, lectureIdx}
				<TableBodyRow>
					<TableBodyCell class="p-2"><GenericValidatedInput type="text" bind:value={lecture.name} validateFn={() => checkDuplicateLecture(lectureIdx)} class="text-2xs"/></TableBodyCell>
					<TableBodyCell class="p-2 text-2xs"><PositiveNumberInput bind:value={lecture.points} class="text-2xs text-center"/></TableBodyCell>
					{#each topic.subtopics as subTopic}
					<TableBodyCell class="p-2"><Checkbox bind:checked={lecture.skills[subTopic]} on:change={() => addSkill(lectureIdx, subTopic)} class="m-auto"/></TableBodyCell>
					{/each}
					<!--<TableBodyCell class="p-2 text-2xs"><Input type="text" bind:value={lecture.description} class="text-2xs"/></TableBodyCell>-->
					<TableBodyCell class="p-2 text-2xs"><Input type="text" bind:value={lecture.description} class="text-2xs"/></TableBodyCell>
					<TableBodyCell class="p-2 text-2xs"><Select items={subjectSelectionItems} bind:value={lecture.subject} class="text-2xs"/></TableBodyCell>	
					<TableBodyCell class="p-2"><Button color="red" size="xs" class="text-2xs" on:click={() => deleteLecture(lectureIdx)}><TrashBinOutline /></Button></TableBodyCell>
				</TableBodyRow>
				{/each}
			</TableBody>
	</Table>
	</div> <!-- -->
	<Button class="text-2xs m-2" on:click={() => addLecture()}>Add Another Lecture</Button>
</div>
{/each}
