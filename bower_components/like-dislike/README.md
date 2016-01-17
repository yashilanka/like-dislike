# like-dislike
A simple jQuery plugin for the create a rating bar with two buttons: Like and Dislike.

## Installation

Type `$ bower install like-dislike` into the command line prompt in your project folder or press "Download ZIP" button on the main GitHub page to get all the files and manually add them to your project.

Load jQuery and a jQuery like-dislike plugin into your document:

```html
<!-- jQuery library -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/2.2.0/jquery.min.js"></script>
<!-- jQuery like-dislike plugin -->
<script src="like-dislike-master/js/like-dislike.js"></script>
```

## Usage

```html
<div id="rating">
  <button class="like">Like</button>
  <span class="likes">0</span>
  <button class="dislike">Dislike</button>
  <span class="dislikes">0</span>
</div>

<script type="text/javascript">
  $('#rating').likeDislike({
    reverseMode: true,
    activeBtn: localStorage['key']? localStorage['key'] : '',
    click: function(btnType, likes, dislikes, event) {
      var self = this;
      
      // lock the buttons
      self.readOnly(true);
      
      // send data to the server
      $.ajax({
        url: '/action',
        type: 'GET',
        data: 'id=1' + '&likes=' + likes + '&dislikes=' + dislikes,
        success: function (data) {
          // show new values
          $(self).find('.likes').text(data.likes);
          $(self).find('.dislikes').text(data.dislikes);
          localStorage['key'] = btnType;

          // unlock the buttons
          self.readOnly(false);
        }
      });
    }
  });
</script>
```

## Options

```javascript

// this function will be called when you push one of the buttons
click: null, // function() {},

// active button ('like' or 'dislike')
activeBtn: null, 

// init plugin with locked ('true') or unlocked ('false') buttons
readOnly: false,

// possibility to cancel vote
reverseMode: false,

// class name of the Like button
likeBtnClass: 'like',

// class name of the Dislike button
dislikeBtnClass: 'dislike',

// class name of the active button
activeClass: 'active',

// class name of the disable button
disableClass: 'disable'

```

## Methods

`readOnly(bool)` Locks or unlocks buttons, depending on the parameter.
 

## Browser support

*Google Chrome
*Firefox 3.5+
*Safari 4+
-IE 8+
-Opera
