Bounding box annotator
======================

A bounding box annotation tool written in CoffeeScript/JavaScript.
There is an online demo at https://kyamagu.github.io/bbox-annotator/demo.html

Contents
--------

    bbox_annotator.coffee  Main code.
    demo.html              Example to host on a private server.
    mturk.html             Example to use in Amazon MTurk.
    README.md              This documentation.

Be sure to unescape `&#215;` with `×` when directly editing an MTurk template on
the Amazon requester UI.

Compile
-------

Compile the coffee script to get a javascript.

    coffee -c bbox_annotator.coffee

Or, go to http://coffeescript.org/ and compile the coffeescript.

Usage
-----

Load the compiled javascript codes inside HTML.

    <script src="bbox_annotator.js" type="text/javascript"></script>

Embed a block element for annotation tool and a form element in HTML.

    <div id="bbox_annotator"></div>
    <input id="annotation_data" name="annotation_data" type="hidden" />

Then, attach a piece of script to launch the annotation tool. The annotator
takes a callback function on change of the annotation data. Use JSON format to
display the value.

    <script type="text/javascript">
    $(document).ready(function() {
      var editor = new BBoxAnnotator({
        url: "/url/to/image.jpg",
        onchange: function(annotation) {
          $("#annotation_data").val(JSON.stringify(annotation));
        }
      });
    });
    </script>

The returned annotation is an array of objects. Here is an example.

    [
      {
        "top": 0,
        "left": 0,
        "width": 100,
        "height": 100,
        "label", "object"
      }
    ]

Check the attached `demo.html` and `mturk.html` for how to use.

Options
-------

The `BBoxAnnotator` object takes options to change its behavior.

 * `id`: CSS selector for the annotator element. Default is `"#bbox_annotator"`.
 * `input_method`: One of the "text", "select", and "fixed". This will change
                   how to input associated annotation text.
 * `labels`: A string, or an array of strings. Set of labels used for suggestion
             in "text" or "select" input. When fixed, only the first element is chosen.
 * `width`: Width of the image. The default is the original width of the image.
 * `height`: Height of the image. The default is the original height of the
             image.
 * `show_label`: Flag to display a label in the box. Default is true for "text"
                 and "select" input, and false for "fixed" input.
 * `border_width`: Size of border around the image. Default is 2. Leaving it 0
                   can make it hard to start annotation around the image border.
 * `multiple`: Defines if multiple boxes could be selected. Default is `true`. 
 * `guide`: Enable vertical and horizontal guide lines. Specify `true`, or
            object that specifies color like `{'color': '#fff'}`.

License
-------

The code may be redistributed under BSD license.
