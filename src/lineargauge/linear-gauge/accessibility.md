
# Accessibility

<!-- markdownlint-disable MD013 -->
Linear gauge provides built-in compliance with the [WAI-ARIA](http://www.w3.org/WAI/PF/aria-practices/) specifications.
WAI-ARIA Accessibility supports are achieved through the attributes like `aria-label`. It helps to provides information about elements in a document for assistive technology.

**Aria-label:**   Attribute provides the text label with some default description for below elements in linear gauge.

<!-- markdownlint-disable MD033 -->
<table>
<tr>
<td><b>Element</b></td>
<td><b>Default description</b></td>
</tr>
<tr>
<td>Gauge Title</td>
<td>Reads the linear gauge title</td>
</tr>
<tr>
<td>Pointer Value</td>
<td>Reads the value of the pointer</td>
</tr>
</table>

  You can change this default description, using `description` property available in [`pointer`](../api/linear-gauge/pointerModel/#description-string) and [`LinearGauge`](../api/linear-gauge/linearGaugeModel/#description-string) object. It helps the screen reader to read for assistive purpose.