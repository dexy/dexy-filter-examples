Slides Filter
-------------

{% from "dexy.jinja" import hl, ext with context -%}

The `slides` filter takes markdown content, like this::

    {{ d['slides.md'] | indent(4) }}


and lets you generate slides using javascript/css slide presentation tools such
as impress.js or deck.js. Just leave 2 blank lines to indicate a new slide
(this is configurable with the `split` setting).

Here is the HTML generated by the `slides` filter with default settings::

    {{ d['slides.md|jinja|slides'] | indent(4) }}

The default settings work for `deck.js <http://imakewebthings.com/deck.js/>`__.

Here is a dexy configuration which inserts content from the `slides.md` source
(as shown above) into a `deck.html` file which is a deck.js template::

    {{ d['dexy.yaml|idio|t']['deck'] | indent(4) }}

{% if ext == '.html' %}

Here are the resulting deck.js slides:

.. raw:: html

    <iframe src="slides/deck.html" style="border: thin solid grey; width: 100%; height: 400px;">
    </iframe>

{% endif %}

To use the `slides` filter with other presentation tools, change the
`slide-header` and `slide-footer` settings to whatever each slide needs to be
wrapped with. Here are settings which work with `impress.js
<http://bartaz.github.io/impress.js>`__::

    {{ d['dexy.yaml|idio|t']['impress'] | indent(4) }}

These header and footer strings are run through `python string interpolation
<http://docs.python.org/2/library/stdtypes.html#string-formatting-operations>`__
before they are wrapped around the content of each slide. Currently there is
one variable available to this interpolation named `number` which gives you the
slide number, starting with slide 1.

{% if ext == '.html' %}

Here are the resulting impress.js slides:

.. raw:: html

    <iframe src="slides/impress.html" style="border: thin solid grey; width: 100%; height: 400px;">
    </iframe>

{% endif %}
