# quilljs-with-rails (A guide only)

```
<!-- Include stylesheet -->
<link href="https://cdn.quilljs.com/1.1.6/quill.snow.css" rel="stylesheet">

<%= form_for :post, remote: true, html: { id: 'some-form' } do |f| %>
  <div class="form-group">
    <%= f.hidden_field :content, required: true %>
    <div id="editor-container" hidden="true"></div>
    <div id="editor"></div>
    <%= f.submit %>
  </div>
<% end %>

<!-- Include the Quill library -->
<script src="https://cdn.quilljs.com/1.1.6/quill.js"></script>

<!-- Initialize Quill editor -->
<script>
  var quill = new Quill('#editor', {
    theme: 'snow'
  });
</script>

```

JavaScript to fill in post content on from submission

```
var form = document.querySelector('#some-form');
var quill = new Quill('#editor', {
  theme: 'snow'
});

form.onsubmit = function() {
  var postContentInput = document.querySelector('#post-content');
  postContentInput.value = quill.root.innerHTML;
};

```

## Then to display the new formatted content we can use sanitize from rails. We should whitelist the same tags that we have in our editor toolbar.

```
raw sanitize content, tags: %w(strong em u s a span p ol ul li br h1 h2 h3 pre blockquote), attributes: %w(href style class spellcheck)
```

Source:  https://harlemsquirrel.github.io/jekyll/update/2016/12/11/rails-and-quill.html
