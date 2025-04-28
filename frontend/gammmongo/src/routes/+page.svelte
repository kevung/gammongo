<script lang="ts">
    import { Button } from "$lib/components/ui/button/index.js";
    import * as Accordion from "$lib/components/ui/accordion/index.js";
    import * as Card from "$lib/components/ui/card/index.js";
    import * as Carousel from "$lib/components/ui/carousel/index.js";
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

<Carousel.Root class="w-full max-w-xs">
    <Carousel.Content>
        {#each Array(5) as _, i (i)}
            <Carousel.Item>
                <div class="p-1">
                    <Card.Root>
                        <Card.Content
                            class="flex aspect-square items-center justify-center p-6"
                        >
                            <span class="text-4xl font-semibold">{i + 1}</span>
                        </Card.Content>
                    </Card.Root>
                </div>
            </Carousel.Item>
        {/each}
    </Carousel.Content>
    <Carousel.Previous />
    <Carousel.Next />
</Carousel.Root>
