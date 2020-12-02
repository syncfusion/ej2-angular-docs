
# Accessibility

Maps provides built-in compliance with the [WAI-ARIA](http://www.w3.org/WAI/PF/aria-practices/) specifications.
WAI-ARIA Accessibility supports are achieved through the attributes like `aria-label`. It helps to provides information
about elements in a document for assistive technology.

**Aria-label:**   Attribute provides the text label with some default description for below elements in maps.

<!-- markdownlint-disable MD033 -->
<table>
<tr>
<td><b>Element</b></td>
<td><b>Default description</b></td>
</tr>
<tr>
<td>Maps container</td>
<td>-</td>
</tr>
<tr>
<td>Maps Title</td>
<td>Reads the maps title</td>
</tr>
<tr>
<td>Maps Subtitle</td>
<td>Reads the maps subtitle</td>
</tr>
<tr>
<td>Legend Title</td>
<td>Reads the legend title</td>
</tr>
</table>

 You can change this default description, using description property available in `Legend`, `TitleSettings`,
 `SubtitleSettings` and `Maps` object. It helps the screen reader to read for assistive purpose.