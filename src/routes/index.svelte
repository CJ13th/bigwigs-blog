<script context="module">
    export const load = async ({fetch}) => {
        const res = await fetch("/posts.json");

        if (res.ok) {
            const {posts} = await res.json()
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


<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>

<pre>{JSON.stringify(posts, null, 2)}</pre>
