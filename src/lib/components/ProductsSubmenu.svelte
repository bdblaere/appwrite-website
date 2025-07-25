<script lang="ts" context="module">
    export type SubmenuItem = {
        name: string;
        href: string;
        description: string;
        icon: string;
        beta?: boolean;
    };

    export type SubLink = {
        label: string;
        href: string;
    };

    export const products: Array<SubmenuItem> = [
        {
            name: 'Auth',
            href: '/products/auth',
            description: 'Secure login with multi-factor auth.',
            icon: '/images/icons/illustrated/dark/auth.png'
        },
        {
            name: 'Databases',
            href: '/docs/products/databases',
            description: 'Scalable and robust databases.',
            icon: '/images/icons/illustrated/dark/databases.png'
        },
        {
            name: 'Storage',
            href: '/products/storage',
            description: 'Advanced compression and encryption.',
            icon: '/images/icons/illustrated/dark/storage.png'
        },
        {
            name: 'Functions',
            href: '/products/functions',
            description: 'Deploy & scale serverless functions.',
            icon: '/images/icons/illustrated/dark/functions.png'
        },
        {
            name: 'Messaging',
            href: '/products/messaging',
            description: 'Set up a full-functioning messaging service.',
            icon: '/images/icons/illustrated/dark/messaging.png'
        },
        {
            name: 'Realtime',
            href: '/docs/apis/realtime',
            description: 'Subscribe and react to any event.',
            icon: '/images/icons/illustrated/dark/realtime.png'
        },
        {
            name: 'Sites',
            href: '/products/sites',
            description: 'The open-source Vercel alternative.',
            icon: '/images/icons/illustrated/dark/sites.png'
        }
    ];

    export const sublinks: Array<SubLink> = [
        {
            label: 'Appwrite vs. Supabase',
            href: '/blog/post/appwrite-compared-to-supabase'
        },
        {
            label: 'Appwrite vs. Firebase',
            href: '/blog/post/open-source-firebase-alternative'
        },
        {
            label: 'Appwrite vs. Vercel',
            href: '/blog/post/open-source-vercel-alternative'
        }
    ];
</script>

<script lang="ts">
    import { trackEvent } from '$lib/actions/analytics';
    import { classNames } from '$lib/utils/classnames';
    import { createDropdownMenu, melt } from '@melt-ui/svelte';
    import Icon from './ui/icon';

    const {
        elements: { trigger, menu, item, overlay },
        states: { open }
    } = createDropdownMenu({
        loop: true
    });

    export let label: string;
</script>

<button
    class={classNames(
        'text-primary focus:text-accent hover:text-accent inline-flex cursor-pointer items-center justify-between outline-none',
        {
            'text-accent': $open
        }
    )}
    use:melt={$trigger}
>
    {label}

    <span
        class={classNames('web-icon-chevron-down block transition-transform', {
            'rotate-180': $open
        })}
    ></span>
</button>

<div
    use:melt={$menu}
    class={classNames(
        'data-[state=closed]:animate-fade-out data-[state=open]:animate-fade-in relative !left-1/2 z-10 mx-auto mt-6 hidden w-full -translate-x-1/2 flex-col items-center p-0 outline-none [max-inline-size:86.875rem] md:flex'
    )}
>
    <div class="is-special-padding w-full rounded-2xl border border-white/8 bg-[#232325] p-6">
        <div class="grid w-full grid-cols-1 place-content-between gap-16 lg:grid-cols-12">
            <div class="col-span-8 -mr-12 pr-12">
                <span
                    class="font-aeonik-fono text-secondary tracking-loose mb-4 block text-xs uppercase"
                    >{label}<span class="text-accent">_</span></span
                >
                <div
                    class="grid grid-flow-col-dense grid-cols-1 gap-2 md:grid-cols-2 md:grid-rows-4"
                >
                    {#each products as product}
                        <a
                            href={product.href}
                            use:melt={$item}
                            onclick={() =>
                                trackEvent(`products-submenu-${product.name.toLowerCase()}-click`)}
                            class="group flex gap-3 rounded-xl p-1 text-white transition-colors outline-none focus:bg-white/8"
                        >
                            <div
                                class="flex size-12 shrink-0 items-center justify-center rounded-lg border border-white/12 bg-white/6"
                            >
                                <img
                                    src={product.icon}
                                    alt={product.name}
                                    class="size-6 grayscale transition-all group-focus:grayscale-0"
                                />
                            </div>
                            <div class="">
                                <span class="text-sub-body text-primary font-medium"
                                    >{product.name}

                                    {#if product.beta}
                                        <span
                                            class="text-caption bg-accent/24 ml-1 rounded px-2 py-1 font-medium text-white"
                                            >Coming soon</span
                                        >
                                    {/if}
                                </span>
                                <p class="text-caption text-secondary text-pretty">
                                    {product.description}
                                </p>
                            </div>
                        </a>
                    {/each}
                </div>
            </div>
            <div class="col-span-4 -ml-12 border-l border-white/6 pl-12">
                <div
                    use:melt={$item}
                    class="group block rounded-2xl border border-white/12 bg-white/6 p-4 outline-none focus-within:bg-white/12"
                >
                    <header class="flex items-center justify-between">
                        <span
                            class="font-aeonik-fono tracking-loose text-primary block text-xs uppercase"
                            >Customer Stories<span class="text-accent">_</span></span
                        >
                        <a
                            href="/blog/category/customer-stories"
                            class="text-secondary text-caption flex items-center"
                            >Read more customer stories <Icon
                                name="chevron-right"
                                class="transition-transform group-hover:translate-x-0.5"
                            ></Icon></a
                        >
                    </header>

                    <a
                        href="/blog/post/customer-story-storealert"
                        class="my-4 flex flex-1 gap-3 outline-none"
                    >
                        <img
                            src="/images/blog/customer-story-storealert/cover.png"
                            alt="Case study cover"
                            class="aspect-[3/1] max-w-[7.5rem] shrink-0 rounded-xl object-cover"
                        />
                        <p class="text-pretty">
                            Appwrited helped reduce development time by 60%, and lower server costs
                            by 40%.
                        </p>
                    </a>
                </div>

                <div class="mt-8">
                    <span
                        class="font-aeonik-fono tracking-loose text-secondary block text-xs uppercase"
                        >Compare Appwrite<span class="text-accent">_</span></span
                    >
                    <div class="mt-3 space-y-3">
                        {#each sublinks as sublink}
                            <a
                                href={sublink.href}
                                class="text-caption text-primary group flex items-center gap-1"
                            >
                                {sublink.label}
                                <span
                                    class="web-icon-chevron-right transition-transform group-hover:translate-x-0.5"
                                ></span>
                            </a>
                        {/each}
                    </div>
                </div>
            </div>
        </div>
    </div>
    <div
        use:melt={$overlay}
        class="data-[state=closed]:animate-fade-out fixed inset-0 bg-black/60"
    ></div>
</div>
