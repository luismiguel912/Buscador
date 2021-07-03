<template>
    <div class="container">
        <div class="search-box">
            <input
                class="search-input"
                type="text"
                name="q"
                placeholder="Search..."
                v-model="query"
                @input="search"
                >
            <ul
                class="result-list"
                :class="resultVisible">
                <li v-for="post in posts" class="result-item">
                    <a href="#" class="result-link">
                        <div class="result-tittle">{{ post.tittle }}</div>
                        <div class="result-content">{{ post.content }}</div>
                    </a>
                </li>
            </ul>
            <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Ipsum nobis beatae porro velit corrupti quas praesentium, voluptas inventore tempora, consequatur culpa alias atque eaque nihil ab autem doloribus possimus reiciendis.</p>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return{
            query: '',
            posts: []
        }
    },
    computed: {
        resultVisible(){
            return ( this.query.length > 0) ? 'show' : 'hide';
        }
    },
    methods: {
        search(){
            console.log(this.query);
            axios.post('/search',{
                q: this.query
            }).then(res =>{
                console.log(res.data);
                this.posts = res.data;
            }).catch( error =>{
                console.log(error);
            })
        }
    }
};
</script>

<style>
    body {
        font-family: sans-serif;
    }
    ::-webkit-scrollbar {
        width: 110px;
    };
    ::-webkit-scrollbar-track {
        background: #f1f1f1;
    };
    ::-webkit-scrollbar-thumb {
        background: #888;
    };
    ::-webkit-scrollbar-hover {
        background: #555;
    };

    .container {
        padding: 30px;
    }

    .search-box {
        position: relative;
        display: flex;
        align-items: center;
        flex-direction: column;
    }

    .search-input {
        width: 600px;
        height: 30px;
        border-radius: 10px;
        border: 0;
        background: #eeeeee;
        padding: 10px 20px;
        font-size: 18px;
        outline: none;
    }

    .result-list.show {
        position: absolute;
        width: 600px;
        list-style: none;
        background: #fff;
        max-height: 250px;
        overflow-y: auto;
        padding: 0;
        top: 40px;
        border-radius: 10px;
        box-shadow: 1px 2px 8px 0px #b5b5b5;
        margin: 7px 0px;
    }

    .result-list.hide {
        display: none;
    }

    .result-item {
        border-bottom: 1px solid #ececec;
    }

    .result-link {
        text-decoration:none;
        color: #333;
        display: block;
        padding: 10px 15px;
    }

    .result-link {
        background: #f9f9f9;
    }

    .result-tittle {
        font-size: 20px;
        font-weight: 600;
    }

    .result-content {
        font-size: 18px;
    }
</style>

