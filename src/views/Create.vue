<template>
<div class= "container mt-5">
    <div class="row">
        <div class="col-md-12">
            <div class="card border-0 rounded shadow">
                <div class="card-body">
                    <h4>Tambah Post</h4>
                    <hr>
                    <form @submit.prevent="store">
                        <div class="form-group">
                            <label for="title" class="front-weight-bold">Title</label>
                            <input type="text" class="form-control" v-model="post.title" placeholder="Masukan Judul Disini">
                            <div v-if ="validation.title" class="mt- 2 alert alert-danger">
                                {{ validation.title[0] }} 
                            </div>                    
                        </div>

                        <div class="form-group">
                            <label for="content" class="front-weight-bold">Content</label>
                            <textarea class="form-control" rows="4" v-model="post.content" placeholder="Masukan Content Disini"></textarea>
                       <div v-if ="validation.content" class="mt- 2 alert alert-danger">
                                {{ validation.content[0] }} 
                            </div>
                        </div>

                        <button type="submit" class="btn btn-primary">Simpan</button>

                    </form>

                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { reactive, ref } from "vue";
import { useRouter } from "vue-router";
import axios from "axios";

export default {
setup() {
    const post = reactive({
        title: "",
        content: "",
    });

    const validation = ref([]);

    const router = useRouter();

    function store() {
        let title = post.title;
        let content = post.content;

        axios.
        post("http://novaagustina.online/backendapi/public/api/post",{
            title : title,
            content : content,
        })
        .then(() => {
            router.push({
                name: "post.index",
            });
        })
        .catch((error) => {
        validation.value = error.respon.data;
        });
    }

    return {
        post,
        validation,
        router,
        store,
    };

    }

 
};
</script>
