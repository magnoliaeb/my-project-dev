<template>
    <div>
        <h2 class="font-bold my-4 px_4 lg: px-2">Popular Tags</h2>
                <ul class="h-72  overflow-y-scroll">
                    <li class="text-gray-900 hover:text-primary-500 hover:bg-gray-200 rounded py-1 lg:px-2 px-4" v-for="(tag, index) in tags" :key="index">
                        <nuxt-link :to="{ name: 'tags-tag', params: { tag: tag }}">
                        <p>#{{ tag }}</p>

                        </nuxt-link>
                    </li>
                </ul>

    </div>
</template>

<script>
    export default {
        data() {
            return {
                 tags: [
                    'javascript','webdev','beginners', 'react',
                    'vue','tutorial','programming', 'python',
                    'css','codenewbie','productivity', 'node',
                    'devops','career','android', 'discuss',
                    'html','typescript','java', 'showdev',
                    'opensource','github','testing', 'aws',
                    'angular','docker','ruby', 'linux', "security", "machinelearning"
                ],
            }
        },
    }
</script>

<style lang="scss" scoped>

</style>

