# Releases:

## Release 0:


- Attach a function to the blur event. The blur event occurs when the following \<input> Field1 loses focus.

Sample Data :
```html
 <body>
 <form>
   <input id="field1" type="text" value="Field 1">
   <input id="field2" type="text" value="Field 2">
 </form>
</body> 
```

- Append a \<p> element with a text message when an \<input> field is changed. Go to the editor

Sample Data :
```html
<body>
  <form  name='demo_form'>
  First name: <input type="text" name="fname"><br>
  Last name: <input type="text" name="lname"><br>
  <input type="submit" value="Submit">
  </form>
</body>
```
- Double click on paragraph to toggle background color. Go to the editor

Sample Data :
```html
 <body>
 <p>Double-click here to change the background color.</p>
 </body>
```

- Find the position of the mouse pointer relative to the left and top edges of the document 

- Display the keyboard key which was pressed in a textbox
-  Set background color of an element when the element (or any elements inside it) gets focus or  loses focus. 

HTML Code:
```html
<body>
 <div>
 First name: <input type="text"><br>
  Last name: <input type="text">
  </div>
</body>
 ```

CSS Code for background color ::
```css
<style>
  .focusedin {
     background: green;
	   }
  .focusedout {
     background: blue;
	   }
</style>
```