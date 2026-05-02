# when we have only one filed in "form" tag 
- we can press enter on that field, and event is triggered for auto submit, without any button with `type='submit'` in form.


# when we have more then one filed in "form" tag 
- we can press enter on that field, and event is not triggered for submit, unless we have a button with `type='submit'` in form.

# To prevent auto submit on pressing enter in any field in form 
- add `type="button"` on button that has `type="submit"` or on all buttons or on all fields in form. 

- add `event.preventDefault()` on the enter key event for the specific field. 