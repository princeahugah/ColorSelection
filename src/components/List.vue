<template>
    <div>
        <div class="selectedItems">
            <strong>Selected Items:&nbsp;&nbsp;</strong> {{ selectedItemNames }}
        </div>
        <ul class="List">
            <li is="ListItem" v-for="item in items" :key="item.name" :item="item" 
                :selectedItems="selectedItems">
                {{ item.name }}
            </li>
        </ul>
    </div>
</template>

<script>
import ListItem from './ListItem';

export default {
    // Implement a feature to allow item selection with the following requirements:
    // 1. Clicking an item selects/unselects it.
    // 2. Multiple items can be selected at a time.
    // 3. Currently selected items should be visually highlighted.
    // 4. Currently selected items' names should be shown at the top of the page.
    // 5. Make sure to avoid unnecessary re-renders.
    name: 'List',

    components: {
        ListItem
    },

    data() {
        return {
            sizes: ['tiny', 'small', 'medium', 'large', 'huge'],
            colors: ['navy', 'blue', 'aqua', 'teal', 'olive', 'green', 'lime', 'yellow', 'orange',
                'red', 'maroon', 'fuchsia', 'purple', 'silver', 'gray', 'black'],
            fruits: ['apple', 'banana', 'watermelon', 'orange', 'peach', 'tangerine', 'pear', 
                'kiwi', 'mango', 'pineapple'],
            selectedItems: []
        };
    },

    computed: {
        selectedItemNames() {
            return this.selectedItems.join(', ');
        },

        items() {
            return this.sizes.reduce(
                (items, size) => [
                    ...items,
                    ...this.fruits.reduce(
                        (acc, fruit) => [
                            ...acc,
                            ...this.colors.reduce(
                                (acc2, color) => [
                                    ...acc2,
                                    {
                                        name: `${size} ${color} ${fruit}`,
                                        color,
                                    },
                                ],
                                [],
                            ),
                        ],
                        [],
                    ),
                ],
                [],
            );
        }
    }
};
</script>

<style scoped>

.List {
  margin: 16px;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
  grid-auto-rows: 60px;
  grid-gap: 16px;
}

.selectedItems {
    margin: 20px;
    color: #001;
    display: flex;
    font-size: 16px;
}

</style>