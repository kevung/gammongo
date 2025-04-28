<script lang="ts">
import { Button } from "$lib/components/ui/button/index.js";
 import * as Accordion from "$lib/components/ui/accordion/index.js";
</script>

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://svelte.dev/docs/kit">svelte.dev/docs/kit</a> to read the documentation</p>

<Button> Click me</Button>

<Accordion.Root type="single">
    <Accordion.Item value="item-1">
        <Accordion.Trigger>Is it accessible?</Accordion.Trigger>
        <Accordion.Content>
            Yes. It adheres to the WAI-ARIA design pattern.
        </Accordion.Content>
    </Accordion.Item>
</Accordion.Root>
