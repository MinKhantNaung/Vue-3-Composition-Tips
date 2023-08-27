
# Vue 3 Composition Api Tips

### ref and reactive
- In ref(), can use variables, arrays and objects. In script, you must use with '.value'
- In reactive, can only use arrays and objects. You can call varialbe name directly.

### Computed
- When you want to modify existing variables, arrays or objects or when you want to modify props from components or views, you should use computed. 
- You must return in computed functions.
- If you directly change variables, arrays or objects, this is the way 
let filterPosts = computed(() => { 

    return posts.value.filter((post) => {  

        return post.category === props.category;

        })  
    })
- if you want to declare a variable and put changes in that variable, this is the way
let allCategories = ref([]);

let getAllCategories = computed(() => {  
      
      posts.value.forEach((post) => {
        
        if (!allCategories.value.includes(post.category)) {
          
          allCategories.value.push(post.category);
        }
    });
    return allCategories.value;
});

## props
- You can give props in components like this 
<VueComponent :posts="posts" />  

- If you want to use only props in blade, you can use like this in script setup
defineProps(['posts'])
  
  - if you want to use props in script setup to modify or change, you can use like this in script setup  
  let props = defineProps(['posts]) **//variable name must be only props**

## Composables
- for reuseable, we must use composables functions.
- example, in name.js
export default function getPosts() {
      
      let posts = ref([]);

      let getPost = () => {
        ............
      }

      // return variables , functions
      return {
        posts,
        getPost
      }
}
- in components and views, you must import composables first, after that, you can assign variables and functions by destructuring like this
let {posts, getPost} = getPosts();



