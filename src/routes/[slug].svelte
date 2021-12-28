<script context="module">
    export const load = async ({fetch, page: {params} }) => {

        const {slug} = params

        const res = await fetch(`/pages/${slug}.json`);

        if (res.ok) {
            const {page} = await res.json()


            return {
                props: {page}
            }
        }

        const { message } = await res.json();
        
        return {
            error: new Error(message)
        }
    }
</script>

<script>
    export let page;

    const {
    content: { html },
  } = page
</script>

<h1 class="text-4xl font-semibold mb-5">{page.title}</h1>

  <article div class="prose">
    {@html html}
  </article>