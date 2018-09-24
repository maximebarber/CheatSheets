# Vue.js

[TOC]

## Vuelidate tools

* Check if input is invalid
```js
v-if="$v.form.age.$invalid"
```

* Check if input has been touched
```js
v-if="$v.form.age.$dirty"
```
/!\ Vuelidate does not automatically change the value of $dirty. We need to listen to the input event.
```js
<input
    @input="$v.form.name.$touch()"
>
```
Or use secial $model property inside the v-model
```js
<input
  v-model="$v.form.name.$model"
>
```

* Check if $invalid AND $dirty are true
```js
v-if="$v.form.age.$error"
```

* Make your validator accept optional fields
```js
field	:
{
    !validators.helpers.req(value)
},
```

* Conditionnal validation
Return a boolean that indicates if the field is valid
```js
email:
{
    email: validators.email,
    required: validators.requiredIf(function ()
    {
        return !!this.form.newsletter
    })
},
```

## Vue properties

* Bind class to input
```js
<input
	:class="{error: $v.form.name.$error, valid: !$v.form.name.$invalid}"
>
```

* Disable button
```js
<button
	:disabled="$v.form.$invalid">Submit
</button>
```

* Blur
Blur event is fired only when an element has lost focus
```js
<input
	@blur="$v.form.age.$touch()"
>
```
