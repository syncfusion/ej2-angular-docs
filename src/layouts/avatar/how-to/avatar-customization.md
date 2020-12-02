# Avatar customization

## Colour customization

The avatar comes with default background colour (grey). This can be easily customized to desired colour
by adding custom class or directly selecting the avatar class from the CSS.

{% tab template="avatar/color", isDefaultActive = "true", sourceFiles="app/**/*.ts,index.css" %}

```typescript

```

{% endtab %}

## Customize avatar sizes

Even though the avatar comes with five predefined sizes, sometimes it's not enough. So, the avatar is
designed in such a way that the width and height will be relative to font-size. By changing the
`font-size` of the avatar element, you can change the width and height automatically.

{% tab template="avatar/custom-size", isDefaultActive = "true", sourceFiles="app/**/*.ts,index.css" %}

```typescript

```

{% endtab %}

## Use various media in avatar

Avatars can be used with a wide variety of media formats like SVG, font-icons, images, letters, words,
etc. Some of them are given below.

{% tab template="avatar/media-formats", isDefaultActive = "true", sourceFiles="app/**/*.ts,index.css" %}

```typescript

```

{% endtab %}

## Dynamic avatar rendering from datasource

We can render avatar component dynamically from a data-source. In this sample we have rendered the avatar component
using a data-source which contains the image source in different sizes dynamically. This is applicable also for
data-source from the server or remote data or AJAX. We have also rendered the avatar using `CSS` property
`background-image` and using image tag.

{% tab template="avatar/angular-avatar", isDefaultActive=true, sourceFiles="app/**/*.ts,index.css" %}

```typescript

```

{% endtab %}
