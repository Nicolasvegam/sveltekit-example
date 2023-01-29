<script lang="ts">
    import { page } from '$app/stores';

    let post: {
        id: number;
        userId: number;
        title: string;
        body: string;
    }

    let user: {
        id: number;
        name: string;
        username: string;
        email: string;
        address: {
            street: string;
            suite: string;
            city: string;
            zipcode: string;
            geo: {
                lat: string;
                lng: string;
            };
        };
        phone: string;
        website: string;
        company: {
            name: string;
            catchPhrase: string;
            bs: string;
        };
    };

   
    async function fetchAPI(){
        await fetch(`https://jsonplaceholder.typicode.com/posts/${$page.params.slug}`)
            .then(response => response.json())
            .then(json => { 
                post = json
                fetchAPIUsers(post.userId)
        } )
    }


    async function fetchAPIUsers(userId: number){
        await fetch(`https://jsonplaceholder.typicode.com/users/${userId}`)
            .then(response => response.json())
            .then(json => {
                user = json  
        })
    }

    fetchAPI();
</script>

  
<h1> {post ? post.title : 'Loading'}</h1>
<h2>{user ? `Hi I'm ${user.name} everyone calls me ${user.username} (#${user.id})` : 'Loading'}</h2>
<h3>{user ? `Reach me at ${user.email} or call me ${user.phone}` : 'Loading'}</h3>
<p>{post ? post.body : 'Loading'}</p>