<template>
    <div id="app" class="container col-md-6 col-md-offset-3">
        <br/>
        <!--<b-form-select v-model="selected" :options="options"> </b-form-select>-->
        <!--<b-form-group id="select2" label="Select 2">-->
            <!--<b-form-select v-model="selected" :options="options" style="z-index: 1000"> </b-form-select>-->
        <!--</b-form-group>-->
        <!--<b-form-group id="select3" label="Select 3">-->
            <!--<b-form-select v-model="selected" :options="options"> </b-form-select>-->
        <!--</b-form-group>-->
        <select name="" id="s1" class="form-control">
            <option v-for="option in options"
                    :value="option.value"
                    v-html="option.text"
                    :disabled="option.disabled"
                    :key="option.value || option.text"
            ></option>
        </select>
        <br>
        <select name="" id="s2" class="selectpicker form-control">
            <option v-for="option in options"
                    :value="option.value"
                    v-html="option.text"
                    :disabled="option.disabled"
                    :key="option.value || option.text"
            ></option>
        </select>

        <!--<div>Selected: <strong>{{ selected }}</strong></div>-->
        <!--<br/>-->
        <!--<br/>-->
        <!--<br/>-->
        <b-table id="my-table" hover striped :items="items"></b-table>
        <button @click="changeData">Change Data</button>
        <button @click="refreshData">Refresh Data</button>

        <b-dropdown id="ddown3" :text="msg" variant="danger" right size="200">
            <b-dropdown-item href="#" @click="changeMsg('Action')">Action</b-dropdown-item>
            <b-dropdown-item href="#">Another action</b-dropdown-item>
            <b-dropdown-item href="#">Something else here</b-dropdown-item>
        </b-dropdown>

    </div>
</template>

<script>
    const tableItems1 = [
        { isActive: true,  age: 40, first_name: 'Dickerson', last_name: 'Macdonald' },
        { isActive: false, age: 21, first_name: 'Larsen', last_name: 'Shaw' },
        { isActive: false, age: 89, first_name: 'Geneva', last_name: 'Wilson' },
        { isActive: true,  age: 38, first_name: 'Jami', last_name: 'Carney' },
        { isActive: false, age: 27, first_name: 'Essie', last_name: 'Dunlap' },
        { isActive: true,  age: 40, first_name: 'Thor', last_name: 'Macdonald' },
        { isActive: false, age: 26, first_name: 'Mitzi', last_name: 'Navarro' },
        { isActive: false, age: 22, first_name: 'Genevive', last_name: 'Wilson' },
        { isActive: true,  age: 38, first_name: 'John', last_name: 'Carney' },
        { isActive: false, age: 29, first_name: 'Dick', last_name: 'Dunlap' }
    ];

    const tableItems2 = [
        { isActive: false,  age: 40, first_name: 'Dickerson', last_name: 'Macdonald' },
        { isActive: true, age: 21, first_name: 'Larsen', last_name: 'Shaw' },
        { isActive: false, age: 89, first_name: 'Geneva', last_name: 'Wilson' },
        { isActive: true,  age: 38, first_name: 'Jami', last_name: 'Carney' },
        { isActive: false, age: 27, first_name: 'Essie', last_name: 'Dunlap' },
        { isActive: false,  age: 40, first_name: 'Thor', last_name: 'Macdonald' },
        { isActive: false, age: 26, first_name: 'Mitzi', last_name: 'Navarro' },
        { isActive: true, age: 22, first_name: 'Genevive', last_name: 'Wilson' },
        { isActive: true,  age: 38, first_name: 'John', last_name: 'Carney' },
        { isActive: true, age: 29, first_name: 'Dick', last_name: 'Dunlap' }
    ];

    const selectOptions = [
        { value: null, text: 'Please select some item' },
        { value: 'a', text: 'This is First option' },
        { value: 'b', text: 'Default Selected Option' },
        { value: 'd', text: 'This one is disabled', disabled: true },
        { value: 'c', text: 'This is another option' }
    ];


    export default {
        name: 'app',
        data () {
            return {
                msg: 'Dropdown',
                items: tableItems1,
                itemsFlag: false,
                selected: null,
                options: selectOptions,
            }
        },
        mounted: function () {
        },
        methods: {
            changeData () {
                setTimeout( function () {
                    if (this.itemsFlag) {
                        this.items = tableItems1;
                    } else {
                        this.items = tableItems2;
                    }
                    this.itemsFlag = ! this.itemsFlag;
                    console.log("data changed");
                    console.log(this.itemsFlag);
                }.bind(this), 1000);
            },
            refreshData () {
                this.$root.$emit('table::refresh', 'my-table');
            },
            changeMsg(msg) {
                this.msg = msg;
            }
        }
    }
</script>

<style>
    .table-striped>tbody>tr:nth-child(odd)>td,
    .table-striped>tbody>tr:nth-child(odd)>th {
        background-color: #f9f9f9;
    }

    .table-hover tbody tr:hover td, .table-hover tbody tr:hover th {
        background-color: #cce5ff;
    }

    select.form-control {
        -moz-appearance: none;
        -webkit-appearance: none;
        appearancce: none;
        background-position: right center;
        background-repeat: no-repeat;
        background-size: 1ex;
        background-origin: content-box;
        background-image: url("data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiIHN0YW5kYWxvbmU9Im5vIj8+CjxzdmcKICAgeG1sbnM6ZGM9Imh0dHA6Ly9wdXJsLm9yZy9kYy9lbGVtZW50cy8xLjEvIgogICB4bWxuczpjYz0iaHR0cDovL2NyZWF0aXZlY29tbW9ucy5vcmcvbnMjIgogICB4bWxuczpyZGY9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkvMDIvMjItcmRmLXN5bnRheC1ucyMiCiAgIHhtbG5zOnN2Zz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciCiAgIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIKICAgdmVyc2lvbj0iMS4xIgogICBpZD0ic3ZnMiIKICAgdmlld0JveD0iMCAwIDM1Ljk3MDk4MyAyMy4wOTE1MTgiCiAgIGhlaWdodD0iNi41MTY5Mzk2bW0iCiAgIHdpZHRoPSIxMC4xNTE4MTFtbSI+CiAgPGRlZnMKICAgICBpZD0iZGVmczQiIC8+CiAgPG1ldGFkYXRhCiAgICAgaWQ9Im1ldGFkYXRhNyI+CiAgICA8cmRmOlJERj4KICAgICAgPGNjOldvcmsKICAgICAgICAgcmRmOmFib3V0PSIiPgogICAgICAgIDxkYzpmb3JtYXQ+aW1hZ2Uvc3ZnK3htbDwvZGM6Zm9ybWF0PgogICAgICAgIDxkYzp0eXBlCiAgICAgICAgICAgcmRmOnJlc291cmNlPSJodHRwOi8vcHVybC5vcmcvZGMvZGNtaXR5cGUvU3RpbGxJbWFnZSIgLz4KICAgICAgICA8ZGM6dGl0bGU+PC9kYzp0aXRsZT4KICAgICAgPC9jYzpXb3JrPgogICAgPC9yZGY6UkRGPgogIDwvbWV0YWRhdGE+CiAgPGcKICAgICB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMjAyLjAxNDUxLC00MDcuMTIyMjUpIgogICAgIGlkPSJsYXllcjEiPgogICAgPHRleHQKICAgICAgIGlkPSJ0ZXh0MzMzNiIKICAgICAgIHk9IjYyOS41MDUwNyIKICAgICAgIHg9IjI5MS40Mjg1NiIKICAgICAgIHN0eWxlPSJmb250LXN0eWxlOm5vcm1hbDtmb250LXdlaWdodDpub3JtYWw7Zm9udC1zaXplOjQwcHg7bGluZS1oZWlnaHQ6MTI1JTtmb250LWZhbWlseTpzYW5zLXNlcmlmO2xldHRlci1zcGFjaW5nOjBweDt3b3JkLXNwYWNpbmc6MHB4O2ZpbGw6IzAwMDAwMDtmaWxsLW9wYWNpdHk6MTtzdHJva2U6bm9uZTtzdHJva2Utd2lkdGg6MXB4O3N0cm9rZS1saW5lY2FwOmJ1dHQ7c3Ryb2tlLWxpbmVqb2luOm1pdGVyO3N0cm9rZS1vcGFjaXR5OjEiCiAgICAgICB4bWw6c3BhY2U9InByZXNlcnZlIj48dHNwYW4KICAgICAgICAgeT0iNjI5LjUwNTA3IgogICAgICAgICB4PSIyOTEuNDI4NTYiCiAgICAgICAgIGlkPSJ0c3BhbjMzMzgiPjwvdHNwYW4+PC90ZXh0PgogICAgPGcKICAgICAgIGlkPSJ0ZXh0MzM0MCIKICAgICAgIHN0eWxlPSJmb250LXN0eWxlOm5vcm1hbDtmb250LXZhcmlhbnQ6bm9ybWFsO2ZvbnQtd2VpZ2h0Om5vcm1hbDtmb250LXN0cmV0Y2g6bm9ybWFsO2ZvbnQtc2l6ZTo0MHB4O2xpbmUtaGVpZ2h0OjEyNSU7Zm9udC1mYW1pbHk6Rm9udEF3ZXNvbWU7LWlua3NjYXBlLWZvbnQtc3BlY2lmaWNhdGlvbjpGb250QXdlc29tZTtsZXR0ZXItc3BhY2luZzowcHg7d29yZC1zcGFjaW5nOjBweDtmaWxsOiMwMDAwMDA7ZmlsbC1vcGFjaXR5OjE7c3Ryb2tlOm5vbmU7c3Ryb2tlLXdpZHRoOjFweDtzdHJva2UtbGluZWNhcDpidXR0O3N0cm9rZS1saW5lam9pbjptaXRlcjtzdHJva2Utb3BhY2l0eToxIj4KICAgICAgPHBhdGgKICAgICAgICAgaWQ9InBhdGgzMzQ1IgogICAgICAgICBzdHlsZT0iZmlsbDojMzMzMzMzO2ZpbGwtb3BhY2l0eToxIgogICAgICAgICBkPSJtIDIzNy41NjY5Niw0MTMuMjU1MDcgYyAwLjU1ODA0LC0wLjU1ODA0IDAuNTU4MDQsLTEuNDczMjIgMCwtMi4wMzEyNSBsIC0zLjcwNTM1LC0zLjY4MzA0IGMgLTAuNTU4MDQsLTAuNTU4MDQgLTEuNDUwOSwtMC41NTgwNCAtMi4wMDg5MywwIEwgMjIwLDQxOS4zOTM0NiAyMDguMTQ3MzIsNDA3LjU0MDc4IGMgLTAuNTU4MDMsLTAuNTU4MDQgLTEuNDUwODksLTAuNTU4MDQgLTIuMDA4OTMsMCBsIC0zLjcwNTM1LDMuNjgzMDQgYyAtMC41NTgwNCwwLjU1ODAzIC0wLjU1ODA0LDEuNDczMjEgMCwyLjAzMTI1IGwgMTYuNTYyNSwxNi41NDAxNyBjIDAuNTU4MDMsMC41NTgwNCAxLjQ1MDg5LDAuNTU4MDQgMi4wMDg5MiwwIGwgMTYuNTYyNSwtMTYuNTQwMTcgeiIgLz4KICAgIDwvZz4KICA8L2c+Cjwvc3ZnPgo=");
    }
</style>
