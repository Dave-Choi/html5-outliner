html5-outliner
==============

Implementation of whatwg spec for outlining HTML5 documents:
http://www.whatwg.org/specs/web-apps/current-work/multipage/sections.html#outlines

Other implementations exist, e.g.:
* http://code.google.com/p/h5o/
* https://github.com/hoyois/html5outliner

I was interested in getting the data in a format I could use for things besides a simple table of contents, though, and wanted to add some functionality for taking the generated hierarchy and making implied sectioning explicit.

Also, the description of the algorithm is presented somewhat unclearly.  That is, object requirements are interspersed throughout its description, and motivation for actions isn't always given.

This is intended to be an implementation with output that conforms to the standard presented, but easier to understand and maintain than a line-by-line translation.

Specifically, the description of the algorithm uses the concept of a **section** as being associated with a set of DOM nodes, and may contain subsections and a heading.  But the concept of an **outline** is presented as a list of sections, apparently as its own object.  However, I think it's more natural to think of an outline as a computed property of a section.

The goal of the algorithm then would simply be to establish a **section** representing the root node, with the appropriate set of subsections.  The outline could then be the output of a **section** method, which would only have to do a simple tree traversal.

Furthermore, the implicitly defined sections could be made explicit by wrapping the nodes in the section in a sectioning element (e.g. `<section>`).