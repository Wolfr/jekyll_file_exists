# Jekyll File Exists

A Jekyll plugin that makes it easily possible to check the existence of a file.

## Installation

Copy `file_exists.rb` into the `/_plugins/` directory of your Jekyll project.

## Usage

### Basic Example

The plugin adds a new custom liquid tag, which can be used as follows:  
`{% file_exists images/file-example.jpg %}`

The output will be `"true"` or `"false"` (a string, not a boolean).

You can also use liquid objects within the tag:  
`{% file_exists {{ author_photo_url }} %}`

**Important:** The path needs to start at the root level of your Jekyll project and without a leading slash `/`.

### Production Example

I’m using the plugin on [My Morning Routine](http://mymorningroutine.com) to check if an author image exists, otherwise Jekyll should use our placeholder image.

#### 1. Check if the file exists AND capture the result

We’re saving the plugins output to `author_photo`:  
`{% capture author_photo %}{% file_exists {{ author_photo_url }} %}{% endcapture %}`

#### 2. Write an if/else clause for the result

If the author photo exists `"true"` we gonna use it, otherwise `"false"` we use the placeholder image.  
```liquid
{% if author_photo == "true" %}
  {% assign author_photo = author_photo_url | prepend: "/" | prepend: site.baseurl %}
{% else %}
  {% assign author_photo = "no-photo.jpg" | prepend: "/images/routines/" | prepend: site.baseurl %}
{% endif %}
```

## Credits

* [Johan Ronsse](https://github.com/Wolfr/jekyll_file_exists)
* [Michael Xander](https://github.com/michaelx)
