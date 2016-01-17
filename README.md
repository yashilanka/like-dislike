# like-dislike

A simple jQuery plugin that allow you to create a rating bar with two buttons: Like and Dislike.

- [Demos](http://uagrace.github.io/like-dislike)


## Installation

If you use [Bower](http://bower.io/search/?q=like-dislike), you can type into the command line prompt in your project folder:

`$ bower install like-dislike` 

Or press "Download ZIP" button on the main GitHub page to get all the files and manually add them to your project.


## Preparation

Add jQuery and jQuery like-dislike plugin into your document:

```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/2.2.0/jquery.min.js"></script>
<script src="like-dislike-master/js/like-dislike.min.js"></script>
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

// this callback function will be called when you push one of the buttons
click: null, // function() {},

// active button ('like' or 'dislike')
activeBtn: null, 

// init plugin with locked or unlocked buttons
readOnly: false,

// possibility to cancel vote
reverseMode: false,

// class name of the like button
likeBtnClass: 'like',

// class name of the dislike button
dislikeBtnClass: 'dislike',

// class name of the active button
activeClass: 'active',

// class name of the disable button
disableClass: 'disable'

```

## Methods

`readOnly(state)` lock or unlock buttons, depending on `state (bool)` parameter.
