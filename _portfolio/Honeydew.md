---
layout: post
title: Honeydew
feature-img: "img/honeydew/Landing-honeydew.png"
thumbnail-path: "img/honeydew/Landing-honeydew.png"
short-description: A task management app designed to be a simple and engaging UI.
---
# Honeydew

This is a task management web app built primarily to emulate [Wunderlist](https://www.wunderlist.com) in some functionality and style. It allows for users to create lists that contain tasks, and each task has its own notes and due date attributes. You can play with this app over [here](https://honeydew-4nier.herokuapp.com).

![first screen](img/honeydew/Landing-honeydew.png)

Honeydew is a Ruby on Rails app utilizing Rails 5.1.4 (as of last update) and Ruby 2.4 . My aim was to create an app with forms that neatly nest within the elements and felt unobtrusive but easy to identify.

![list show](img/honeydew/list-show.png)

To that end, some styling was provided simply with css, as is the case with the drop down log-in.

![log-in clip](img/honeydew/log-in.jpg)

But for other elements, it was achieved through jQuery. The collapsable sidebar-

![menu collapsed](img/honeydew/menu-collapsed.jpg)

is operated like so:

``` javascript
$(document).ready(function () {

    $('#sidebarCollapse').on('click', function () {
        $('#sidebar').toggleClass('active');
    });

});
```

Very similar scripts operate the notes and due date sections for each task.

![note closed](img/honeydew/note-closed.jpg)
![note open](img/honeydew/note-open.jpg)

An important difference though, is that because each task needed its own identifier in order to operate.

![many notes open](img/honeydew/many-notes.jpg)

Changing the identifier to be dynamic, allows for an easy solution:

```html
<div class="note-text-field" id="note-div-task-<%= task.id %>">
  <%= form.text_area :notes, class: "task-note-field", rows: '4', placeholder: "Enter task notes here", id: "task-note" %>
  <%= form.submit "update", class: "add-note-btn"%>
</div>

```
``` javascript

$(document).ready(function () {
  $(".glyphicon-book").on('click', function() {
    var taskElement = "#note-div-task-" + $(this).data('task-id');
    $(taskElement).fadeToggle();
    $(taskElement + " .task-note-field").focus();
  });
});

```

As far as style goes, I owe a debt of gratitude to both Pixabay and Unsplash from some fantastic free use images. With a background image I liked, I was able to utilize Coolors.co, whose color scheme generator- which saved me a bunch of time selecting the right colors.

Check below for links to those.

## Areas still developing

* sizing for different devices.  
* organization of tasks by due date-field.  
* different visuals for items close to due, and items past due.  
* ability to choose avatar outside of gravatar import.
* customizable color scheme/background.  

## Authors

* **Michael Fournier** - *Initial work* - [Cloud974](https://github.com/Cloud974)

## Acknowledgments

* [Pixabay](https://www.pixabay.com) - "Pixabay is a vibrant community of creatives, sharing copyright free images and videos."
* [Unsplash](https://www.unsplash.com) - "Beautiful, free photos. Gifted by the world’s most generous community of photographers."
* [Heroku](https://www.heroku.com) - "Heroku is a platform as a service (PaaS) that enables developers to build, run, and operate applications entirely in the cloud."
* [Coolors](https://coolors.co) - "The super fast color schemes generator!"
