---
title: "How To Section For Avatar"
component: "Avatar"
description: "Avatar how to section, avatar color & size customization, media format as avatar content, avatar integration with ListView (gmail list avatar) & business cards."
---

# How To

As the avatar is a completely customizable and integral component, this section shows some of the
customization and integration of avatar with other components.

## Customize avatars

### Colour customization

The avatar comes with default background colour (grey). This can be easily customized to desired colour
by adding custom class or directly selecting the avatar class from the CSS.

{% tab template="avatar/color", isDefaultActive = "true", sourceFiles="app/**/*.ts,index.css" %}

```typescript

```

{% endtab %}

### Customize avatar sizes

Even though the avatar comes with five predefined sizes, sometimes it's not enough. So, the avatar is
designed in such a way that the width and height will be relative to font-size. By changing the
`font-size` of the avatar element, you can change the width and height automatically.

{% tab template="avatar/custom-size", isDefaultActive = "true", sourceFiles="app/**/*.ts,index.css" %}

```typescript

```

{% endtab %}

### Use various media in avatar

Avatars can be used with a wide variety of media formats like SVG, font-icons, images, letters, words,
etc. Some of them are given below.

{% tab template="avatar/media-formats", isDefaultActive = "true", sourceFiles="app/**/*.ts,index.css" %}

```typescript

```

{% endtab %}

### Dynamic avatar rendering from datasource

We can render avatar component dynamically from a data-source. In this sample we have rendered the avatar component
using a data-source which contains the image source in different sizes dynamically. This is applicable also for
data-source from the server or remote data or AJAX. We have also rendered the avatar using `CSS` property
`background-image` and using image tag.

{% tab template="avatar/angular-avatar", isDefaultActive=true, sourceFiles="app/**/*.ts,index.css" %}

```typescript

```

{% endtab %}

## Integrate avatars

Avatar can be integrated into various components to make a wide variety of applications. Some of the
integrations are shown in the following section.

### Listview

Avatar is integrated into the listview to create contacts applications. The `xsmall` size avatar is
used to match the size of the list item. Letters and images are also used as avatar content.

{% tab template="avatar/listview", isDefaultActive = "true", sourceFiles="app/**/*.ts,index.css" %}

```typescript

```

{% endtab %}

### Badge

The badge is dependent and supportive component, and it can be used with avatar to create a notification avatar.
The default avatar (.`e-avatar`) and circle avatar (.`e-avatar-circle`) have been used with notification
badges (.`e-badge-notification`) in the following sample.

{% tab template="avatar/badge", isDefaultActive = "true", sourceFiles="app/**/*.ts,index.css" %}

```typescript

```

{% endtab %}