Tag Cloud: A Plugin for Pelican
===============================

[![Build Status](https://img.shields.io/github/workflow/status/pelican-plugins/tag-cloud/build)](https://github.com/pelican-plugins/tag-cloud/actions)
[![PyPI Version](https://img.shields.io/pypi/v/pelican-tag-cloud)](https://pypi.org/project/pelican-tag-cloud/)
![License](https://img.shields.io/pypi/l/pelican-tag-cloud?color=blue)

This Pelican plugin generates a tag cloud from post tags.

Installation
------------

This plugin can be installed via:

    python -m pip install pelican-tag-cloud

For more detailed plugin installation instructions, please refer to the [Pelican Plugin Documentation](https://docs.getpelican.com/en/latest/plugins.html).

In order to use to use this plugin, you must edit your theme’s base template and style-sheet. You should change **base.html** to apply formats (and sizes) defined in **style.css**, as specified in _Settings_ below.

Settings
--------

| Settings and their default values  |                   What does it do?                    |
| ---------------------------------- | ----------------------------------------------------- |
| `TAG_CLOUD_STEPS = 4`              |  Count of different font sizes in the tag cloud       |
| `TAG_CLOUD_MAX_ITEMS = 100`        |  Maximum number of tags in the cloud                  |
| `TAG_CLOUD_SORTING = "random"`     |  Tag cloud ordering scheme. Valid values: random, alphabetically, alphabetically-rev, size, and size-rev |
| `TAG_CLOUD_BADGE = True`           |  Optional setting: turn on **badges**, displaying the number of articles using each tag |

Usage
-----

The default theme does not include a tag cloud, but it is fairly easy to add one:

```jinja2
<ul class="tagcloud">
    {% for tag in tag_cloud %}
        <li class="tag-{{ tag.1 }}">
            <a href="{{ SITEURL }}/{{ tag.0.url }}">
            {{ tag.0 }}
                {% if TAG_CLOUD_BADGE %}
                    <span class="badge">{{ tag.2 }}</span>
                {% endif %}
            </a>
        </li>
    {% endfor %}
</ul>
```

You should then also define CSS styles with appropriate classes (tag-1 to tag-N, where N matches `TAG_CLOUD_STEPS`), tag-1 being the most frequent, and define a `ul.tagcloud` class with appropriate list-style to create the cloud. You should copy+paste this **badge** CSS rule `ul.tagcloud .list-group-item <span>.badge` if you are using the `TAG_CLOUD_BADGE` setting. (This rule, potentially long, is suggested to avoid conflicts with CSS frameworks such as Twitter Bootstrap.)

For example:

```css
ul.tagcloud {
    list-style: none;
    padding: 0;
}

ul.tagcloud li {
    display: inline-block;
}

li.tag-1 {
    font-size: 150%;
}

li.tag-2 {
    font-size: 120%;
}

/* ... add li.tag-3 etc, as much as needed */

ul.tagcloud .list-group-item span.badge {
    background-color: grey;
    color: white;
}
```

By default, the tags in the cloud are sorted randomly, but if you prefer to have them sorted alphabetically, use `alphabetically` (ascending) and `alphabetically-rev` (descending). Also, it is possible to sort the tags by frequency (number of articles with this specific tag) using the values `size` (ascending) and `size-rev` (descending).

Contributing
------------

Contributions are welcome and much appreciated. Every little bit helps. You can contribute by improving the documentation, adding missing features, and fixing bugs. You can also help out by reviewing and commenting on [existing issues][].

To start contributing to this plugin, review the [Contributing to Pelican][] documentation, beginning with the **Contributing Code** section.

[existing issues]: https://github.com/pelican-plugins/tag-cloud/issues
[Contributing to Pelican]: https://docs.getpelican.com/en/latest/contribute.html

License
-------

This project is licensed under the AGPL-3.0 license.
