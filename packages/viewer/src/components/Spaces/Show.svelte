<script lang="ts">
  import type { Space } from '@/models'
  import { Aliases, Link, References, Source, Tabs, Typeset } from '../Shared'
  import Counterexamples from './Counterexamples.svelte'
  import Properties from './Properties.svelte'

  export let space: Space
  export let tab: 'properties' | 'theorems' | 'references'
  export let rel: string | undefined = undefined

  const tabs = ['properties', 'theorems', 'references'] as const
</script>

<h3>Space <Link.Space {space} content="idLong" /></h3>

<h1>
  <Typeset body={space.name} />
</h1>

{#if space.aliases.length > 0}
  <h4 class="text-muted lead">
    Also known as: <Aliases aliases={space.aliases} />
  </h4>
{/if}

<section class="description">
  <Typeset body={space.description} />
</section>

<section class="description-markdown">
  <Source source={space.description} internal external />
</section>

<Tabs {tabs} {tab} {rel} />

{#if tab === 'properties'}
  <Properties {space} />
{:else if tab === 'theorems'}
  <Counterexamples {space} />
{:else if tab === 'references'}
  <References references={space.refs} />
{:else if tab === 'markdown'}
  <pre>{space.description}</pre>
{/if}
