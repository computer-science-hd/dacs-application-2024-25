<script lang="ts">
	import { Card, Heading, P } from 'flowbite-svelte';

	import FormExtentDetails from '$lib/components/FormExtentDetails.svelte';
	import FormTableTopics from '$lib/components/FormTableTopics.svelte';
	import FormLectureAssigment from '$lib/components/FormLectureAssigment.svelte';
	import FormTableQuestions from '$lib/components/FormTableQuestions.svelte';

	import ButtonDownloadData from '$lib/components/ButtonDownloadData.svelte';

</script>

<div class="flex flex-col md:container md:mx-auto m-2 items-center">
	<Heading class="my-2 p-4 text-center">Skills, Lectures, and Motivation</Heading>
	
	<Card size="xl" class="my-2">
<P>
The admission regulations require you to provide evidence for subject-specific skills worth at least 56 ECTS credit points in computer science and at least 16 ECTS credit points in mathematics. The information you supply in this form is used to provide this evidence.
</P>
<br>
<P>
Once you have filled this form, click "Save form data" at the bottom of this page to save its contents to a file on your computer (in your download folder). Subsequently, upload this file as part of your application in the application portal heiCO.
All data you enter stay within your browser, i.e., your contents are not sent to any server.
</P>
	</Card>
	
	<Card size="xl" class="my-2">
		<Heading tag="h3" class="mb-4 text-center">Details on Field of Study</Heading>
		<FormExtentDetails />
	</Card>

	<Card size="xl" class="my-2">
		<Heading tag="h3" class="mb-4 text-center">Lectures and Skills</Heading>
		<FormTableTopics />
	</Card>

<!--	<Card size="xl" class="my-2">
		<Heading tag="h3" class="mb-4 text-center">Lecture Assignment</Heading>
		<FormLectureAssigment />
	</Card>
-->

	<Card size="xl" class="my-2">
		<Heading tag="h3" class="mb-4 text-center">Motivation</Heading>
		<FormTableQuestions />
	</Card>
	<ButtonDownloadData />
	<!--<Card size="xl" class="my-2"></Card>
		<ButtonDownloadData />
	</Card>-->
</div>
