<script lang="ts">
    import { Button, buttonVariants } from "$lib/components/ui/button/index.js";
    import * as Accordion from "$lib/components/ui/accordion/index.js";
    import * as Card from "$lib/components/ui/card/index.js";
    import * as Carousel from "$lib/components/ui/carousel/index.js";
    import * as Breadcrumb from "$lib/components/ui/breadcrumb/index.js";
    import * as DropdownMenu from "$lib/components/ui/dropdown-menu/index.js";
    import { Checkbox } from "$lib/components/ui/checkbox/index.js";
    import { getLocalTimeZone, today } from "@internationalized/date";
    //import { Calendar } from "$lib/components/ui/calendar/index.js";
    import Check from "@lucide/svelte/icons/check";
    import ChevronsUpDown from "@lucide/svelte/icons/chevrons-up-down";
    import { tick } from "svelte";
    import * as Command from "$lib/components/ui/command/index.js";
    import * as Popover from "$lib/components/ui/popover/index.js";
    import { cn } from "$lib/utils.js";
    import * as Dialog from "$lib/components/ui/dialog/index.js";
    import { Input } from "$lib/components/ui/input/index.js";
    import { Label } from "$lib/components/ui/label/index.js";
    import Calendar from "@lucide/svelte/icons/calendar";
    // import * as CalendarIcon from "@lucide/svelte/icons/calendar";
    import * as Avatar from "$lib/components/ui/avatar/index.js";
    import * as HoverCard from "$lib/components/ui/hover-card/index.js";

    let value_calendar = today(getLocalTimeZone());


    const frameworks = [
        {
            value: "sveltekit",
            label: "SvelteKit"
        },
        {
            value: "next.js",
            label: "Next.js"
        },
        {
            value: "nuxt.js",
            label: "Nuxt.js"
        },
        {
            value: "remix",
            label: "Remix"
        },
        {
            value: "astro",
            label: "Astro"
        }
    ];

    let open = $state(false);
    let value = $state("");
    let triggerRef = $state<HTMLButtonElement>(null!);

    const selectedValue = $derived(
        frameworks.find((f) => f.value === value)?.label
    );

    // We want to refocus the trigger button when the user selects
    // an item from the list so users can continue navigating the
    // rest of the form with the keyboard.
    function closeAndFocusTrigger() {
        open = false;
        tick().then(() => {
            triggerRef.focus();
        });
    }

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

<Breadcrumb.Root>
    <Breadcrumb.List>
        <Breadcrumb.Item>
            <Breadcrumb.Link href="/">Home</Breadcrumb.Link>
        </Breadcrumb.Item>
        <Breadcrumb.Separator />
        <Breadcrumb.Item>
            <DropdownMenu.Root>
                <DropdownMenu.Trigger class="flex items-center gap-1">
                    <Breadcrumb.Ellipsis class="size-4" />
                    <span class="sr-only">Toggle menu</span>
                </DropdownMenu.Trigger>
                <DropdownMenu.Content align="start">
                    <DropdownMenu.Item>Documentation</DropdownMenu.Item>
                    <DropdownMenu.Item>Themes</DropdownMenu.Item>
                    <DropdownMenu.Item>GitHub</DropdownMenu.Item>
                </DropdownMenu.Content>
            </DropdownMenu.Root>
        </Breadcrumb.Item>
        <Breadcrumb.Separator />
        <Breadcrumb.Item>
            <Breadcrumb.Link href="/docs/components">Components</Breadcrumb.Link>
        </Breadcrumb.Item>
        <Breadcrumb.Separator />
        <Breadcrumb.Item>
            <Breadcrumb.Page>Breadcrumb</Breadcrumb.Page>
        </Breadcrumb.Item>
    </Breadcrumb.List>
</Breadcrumb.Root>

	
<Checkbox />

// <Calendar type="single" bind:value_calendar class="rounded-md border" />

<Popover.Root bind:open>
    <Popover.Trigger bind:ref={triggerRef}>
        {#snippet child({ props })}
            <Button
                variant="outline"
                class="w-[200px] justify-between"
                {...props}
                role="combobox"
                aria-expanded={open}
            >
                {selectedValue || "Select a framework..."}
                <ChevronsUpDown class="opacity-50" />
            </Button>
        {/snippet}
    </Popover.Trigger>
    <Popover.Content class="w-[200px] p-0">
        <Command.Root>
            <Command.Input placeholder="Search framework..." />
            <Command.List>
                <Command.Empty>No framework found.</Command.Empty>
                <Command.Group>
                    {#each frameworks as framework (framework.value)}
                        <Command.Item
                            value={framework.value}
                            onSelect={() => {
                                value = framework.value;
                                closeAndFocusTrigger();
                            }}
                        >
                            <Check
                                class={cn(value !== framework.value && "text-transparent")}
                            />
                            {framework.label}
                        </Command.Item>
                    {/each}
                </Command.Group>
            </Command.List>
        </Command.Root>
    </Popover.Content>
</Popover.Root>

<Dialog.Root>
    <Dialog.Trigger class={buttonVariants({ variant: "outline" })}
    >Edit Profile</Dialog.Trigger
>
    <Dialog.Content class="sm:max-w-[425px]">
        <Dialog.Header>
            <Dialog.Title>Edit profile</Dialog.Title>
            <Dialog.Description>
                Make changes to your profile here. Click save when you're done.
            </Dialog.Description>
        </Dialog.Header>
        <div class="grid gap-4 py-4">
            <div class="grid grid-cols-4 items-center gap-4">
                <Label for="name" class="text-right">Name</Label>
                <Input id="name" value="Pedro Duarte" class="col-span-3" />
            </div>
            <div class="grid grid-cols-4 items-center gap-4">
                <Label for="username" class="text-right">Username</Label>
                <Input id="username" value="@peduarte" class="col-span-3" />
            </div>
        </div>
        <Dialog.Footer>
            <Button type="submit">Save changes</Button>
        </Dialog.Footer>
    </Dialog.Content>
</Dialog.Root>

<HoverCard.Root>
    <HoverCard.Trigger
        href="https://github.com/sveltejs"
        target="_blank"
        rel="noreferrer noopener"
        class="rounded-sm underline-offset-4 hover:underline focus-visible:outline-2 focus-visible:outline-offset-8 focus-visible:outline-black"
    >
        @sveltejs
    </HoverCard.Trigger>
    <HoverCard.Content class="w-80">
        <div class="flex justify-between space-x-4">
            <Avatar.Root>
                <Avatar.Image src="https://github.com/sveltejs.png" />
                <Avatar.Fallback>SK</Avatar.Fallback>
            </Avatar.Root>
            <div class="space-y-1">
                <h4 class="text-sm font-semibold">@sveltejs</h4>
                <p class="text-sm">Cybernetically enhanced web apps.</p>
                <div class="flex items-center pt-2">
                    <Calendar class="mr-2 size-4 opacity-70" />
                    <span class="text-muted-foreground text-xs">
                        Joined September 2022
                    </span>
                </div>
            </div>
        </div>
    </HoverCard.Content>
</HoverCard.Root>
