
# Accessibility

The tree map control provides built-in compliance with [WAI-ARIA](http://www.w3.org/WAI/PF/aria-practices/) specifications. WAI-ARIA accessibility supports are achieved using attributes such as `aria-label`. It helps to provide information about elements in a document for assistive technology.

**Aria-label:**

This attribute provides the text label with some default description for the following elements in tree map.

<!-- markdownlint-disable MD033 -->
<table>
<tr>
<td><b>Element</b></td>
<td><b>Default description</b></td>
</tr>
<tr>
<td>TreeMap container</td>
<td>-</td>
</tr>
<tr>
<td>TreeMap Title</td>
<td>Reads the tree map title</td>
</tr>
<tr>
<td>TreeMap Subtitle</td>
<td>Reads the tree map subtitle</td>
</tr>
<tr>
<td>Legend Title</td>
<td>Reads the legend title</td>
</tr>
</table>

You can change this default description using the description property available in `Legend`, `TitleSettings`, `SubtitleSettings`, and `TreeMap` objects. It helps screen readers to read for assistive purpose.
