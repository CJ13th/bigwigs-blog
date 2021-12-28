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


<h1 class="text-4xl mb-10 font-extrabold">Bigwigs Blog</h1>

{#each posts as {title, slug, excerpt, coverImage, tags}}
    <div class="card text-center shadow-2xl mb-20">
        <figure class="px-10 pt-10">
            <img src={coverImage.url} alt={`Cover image for ${title}`}>
        </figure>
    </div>
    <div class="card-body">
        <h1 class="title">{title}</h1>
        <p>{excerpt}</p>
        {#each tags as tag}
            <div class="flex justify-center mt-5 space-x-2">
                <span class="badge badge-primary">{tag}</span>
            </div>
        {/each}
        <div class="justify-center card-actions">
            <a href={`/posts/${slug}`} class="btn btn-outline btn-primary">Read more</a>
        </div>
    </div>

{/each}

