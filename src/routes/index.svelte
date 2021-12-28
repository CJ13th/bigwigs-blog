<script context="module">
    export const load = async ({fetch}) => {
        const res = await fetch("/posts.json");

        if (res.ok) {
            const {posts} = await res.json()
            console.log(res.ok)
            return {
                props: {posts}
            }
        }

        const { message } = await res.json();
        
        return {
            error: new Error(message)
        }
    }
</script>

<script>
    export let posts;
</script>


<h1 class="text-4xl mb-10 font-extrabold">Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>

{#each posts as post}
    <pre>{post.title}</pre>
{/each}