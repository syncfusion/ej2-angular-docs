---
title: "Types Of Badge"
component: "Badge"
description: "Angular pure CSS Badge component has eight (8) types of badges, namely circle, pill, link, notification, overlap, dot, and position."
---

# Types and Styles

This section explains different styles and types of the badges.

## Badge styles

The Essential JS 2 Badge has the following predefined styles that can be used with `.e-badge` class to change the appearance of a badge.

| Class Name        | Description
| :-------------    |:-------------
| e-badge-primary   | Represents a primary notification.
| e-badge-secondary | Represents a secondary notification.
| e-badge-success   | Represents a positive notification.
| e-badge-danger    | Represents a negative notification.
| e-badge-warning   | Represents notification with caution.
| e-badge-info      | Represents an informative notification.
| e-badge-light     | Represents notification in light variant.
| e-badge-dark      | Represents notification in dark variant.

{% tab template="badge/types", isDefaultActive = "true", sourceFiles="app/**/*.ts", index.css" %}

```typescript

```

{% endtab %}

## Badge types

The types of Essential JS 2 badges are as follows:

* Circle
* Pill
* Link
* Notification
* Overlap
* Dot
* Position

### Circle

The circle badge style can be applied by adding the modifier class `.e-badge-circle` to the target element.

{% tab template="badge/circle", isDefaultActive = "true", sourceFiles="app/**/*.ts", index.css" %}

```typescript

```

{% endtab %}

### Pill

The pill badge style can be applied by adding the modifier class `.e-badge-pill` to the target element.

{% tab template="badge/pill", isDefaultActive = "true", sourceFiles="app/**/*.ts", index.css" %}

```typescript

```

{% endtab %}

### Link

When badge modifier classes are applied to the anchor tag, the badge’s appearance will change from normal state to hover state on mouseover.

{% tab template="badge/link", isDefaultActive = "true", sourceFiles="app/**/*.ts", index.css" %}

```typescript

```

{% endtab %}

### Notification

The notification badge style can be applied by adding the modifier class `.e-badge-notification` to the
target element. Notification badges are used when a content or a context needs special attention.
While using the notification badge, set the parent element to `position: relative`.

{% tab template="badge/notification", isDefaultActive = "true", sourceFiles="app/**/*.ts", index.css" %}

```typescript

```

{% endtab %}

### Dot

Dot can be applied by adding the modifier class `.e-badge-dot` to the target element. Dot badges are
similar to notification badges, but in a minimalistic way. While using the dot badge, set the parent
element to `position: relative` .

{% tab template="badge/dot", isDefaultActive = "true", sourceFiles="app/**/*.ts", index.css" %}

```typescript

```

{% endtab %}

### Overlap

The overlap badge can be used with `notification` or `dot` badge, which overlaps with the target
-element by adding the modifier class `.e-badge-overlap`. While using the overlap badge, set the
parent element to `position: relative`.

{% tab template="badge/overlap", isDefaultActive = "true", sourceFiles="app/**/*.ts", index.css" %}

```typescript

```

{% endtab %}

### Position

The default position of the `notification` or `dot` badge is top. But, the position can be changed
to `bottom` using the modifier class `.e-badge-bottom`. For example, the bottom class modifier is used
with dot badge to display the status in the avatar as shown in the following sample.

{% tab template="badge/position", isDefaultActive = "true", sourceFiles="app/**/*.ts", index.css" %}

```typescript

```

{% endtab %}
