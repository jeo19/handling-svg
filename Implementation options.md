> # One thing that should be noticed before handling svg.

one thing that is often forgotten about, remember to enable gzip compression for SVGs on your websites in the .htaccess file.

<pre>
AddType image/svg+xml svg svgz
<IfModule mod_deflate.c>
    <IfModule mod_filter.c>
        AddOutputFilterByType DEFLATE "image/svg+xml" \
                                      "text/css" \
                                      "text/html" \
                                      "text/javascript"
                                      ... etc
    </IfModule>
</IfModule>
</pre>

> # Implementation options

### Img

    Just as you would with any other image. You can also use SVGs in a <picture> element. Note that this method limits manipulation functionality.

```html
<img src="bblogo.svg" alt="Breaking Borders Logo" height="65" width="68" />
```

### Background-image

    It’s best not to base64 encode them as it this will block the loading of the rest of the styles while it downloads. Note that this method limits manipulation functionality.

```css
.logo {
  background-image: url(bblogo.svg);
}
```

### Embed

    <embed> is meant to be used to integrate ‘an external application’ or ‘interactive content’. You can use it for SVGs but yea probably just don’t.

```html
<embed type="image/svg+xml" src="bblogo.svg" />
```

### Object

    <object> is pretty much the best option to use if you want to be able to manipulate an SVG without having to put it inline in your HTML.

```html
<object type="image/svg+xml" data="bblogo.svg"
  >Your browser does not support SVGs</object
>
```

### Inline

    Putting your SVG code inline will save an HTTP request but it will mean the image isn’t cached by the browser. It is the easiest way to manipulate, however maintaining inline SVG code can be a pain.

```html
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 68 65">
  <path
    fill="#1A374D"
    d="M42 27v-20c0-3.7-3.3-7-7-7s-7 3.3-7 7v21l12 15-7 15.7c14.5 13.9 35 2.8 35-13.7 0-13.3-13.4-21.8-26-18zm6 25c-3.9 0-7-3.1-7-7s3.1-7 7-7 7 3.1 7 7-3.1 7-7 7z"
  />
  <path
    d="M14 27v-20c0-3.7-3.3-7-7-7s-7 3.3-7 7v41c0 8.2 9.2 17 20 17s20-9.2 20-20c0-13.3-13.4-21.8-26-18zm6 25c-3.9 0-7-3.1-7-7s3.1-7 7-7 7 3.1 7 7-3.1 7-7 7z"
  />
</svg>
```

### To conclude

    If you want to get the most out of your SVGs use <object>. Alternatively you can use them inline to save the HTTP request, but note that it will not be cached. If you just want to use SVGs as you would any other image use <img> or a background-image. You have the ability to use <iframe> and <embed> but I don’t think they are the best options going forward (and for the purposes of this site, I will not focus on them any longer).

<table id="implementation-support">
<thead>
<tr>
<th></th>
<th>Object</th>
<th>Inline</th>
<th>Img</th>
<th>Background-image</th>
</tr>
</thead>
<tbody>
<tr>
<th class="feature"><span class="small-caps">CSS</span> Manipulation</th>
<td>Yes</td>
<td>Yes</td>
<td>Some inline</td>
<td>Some inline</td>
</tr>
<tr>
<th class="feature"><span class="small-caps">JS</span> Manipulation</th>
<td>Yes</td>
<td>Yes</td>
<td>No</td>
<td>No</td>
</tr>
<tr>
<th class="feature"><span class="small-caps">SVG</span> Animation</th>
<td>Yes</td>
<td>Yes</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<th class="feature">Interactive <span class="small-caps">SVG</span> Animation</th>
<td>Yes</td>
<td>Yes</td>
<td>No</td>
<td>No</td>
</tr>
</tbody>
</table>
