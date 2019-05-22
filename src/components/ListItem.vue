<template>
    <li @click.stop.prevent="handleSelectUnselect(item)"
        :class="['List__item List__item--' + item.color, isSelected]">
        {{ item.name }}
    </li>
</template>

<script>
export default {
    name: 'ListItem',

    data() {
        return {
            selected: false
        };
    },

    props: {
        item: {
            required: true,
            type: Object
        },

        selectedItems: {
            required: true,
            type: Array
        }
    },

    computed: {
        isSelected() {
            return this.selected ? 'active' : '';
        }
    },

    methods: {
        handleSelectUnselect(item) {
            const itemIndex = this.selectedItems.findIndex(itemName => itemName === item.name);
            // if an item already exists, remove it and unselect it
            if (itemIndex > -1) {
                this.selectedItems.splice(itemIndex, 1);
                this.selected = false;
            }
            // if an item does not exist, add it and select it
            else {
                this.selectedItems.push(item.name);
                this.selected = true;
            }
        }
    }
};
</script>

<style scoped>

.List__item {
  line-height: 60px;
  text-align: center;
  color: white;
  text-shadow: 1px 1px rgba(0, 0, 0, 0.5);
  box-shadow: 0px 1px 1px 0px rgba(0, 0, 0, 0.05);
}

.List__item.active {
  border: 4px dashed #FFF;
}

.List__item:hover {
  cursor: pointer;
}

/* Taken from https://clrs.cc/ */

.List__item--navy {
  background-color: #001f3f;
}

.List__item--blue {
  background-color: #0074d9;
}

.List__item--aqua {
  background-color: #7fdbff;
}

.List__item--teal {
  background-color: #39cccc;
}

.List__item--olive {
  background-color: #3d9970;
}

.List__item--green {
  background-color: #2ecc40;
}

.List__item--lime {
  background-color: #01ff70;
}

.List__item--yellow {
  background-color: #ffdc00;
}

.List__item--orange {
  background-color: #ff851b;
}

.List__item--red {
  background-color: #ff4136;
}

.List__item--maroon {
  background-color: #85144b;
}

.List__item--fuchsia {
  background-color: #f012be;
}

.List__item--purple {
  background-color: #b10dc9;
}

.List__item--black {
  background-color: #111111;
}

.List__item--gray {
  background-color: #aaaaaa;
}

.List__item--silver {
  background-color: #dddddd;
}

</style>