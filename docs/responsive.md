# Responsive

Tachyons css is responsive to the core.
The majority of classes include responsive variants that target different breakpoints.
It's important to note that since all classes are functional, responsive variants have different names using a media query naming conventions.

```.html
<div class="pa3 bg-black white">
  <span class="dn-m">Small</span>
  <span class="dn db-m dn-l">Medium</span>
  <span class="dn db-l">Large</span>
</div>
```

### Naming convention

Let's consider the class `.db` which declares `display: block;`:

- `db`: The base class which targets all viewports
- `db-m`: Targets all medium and large viewports
- `db-l`: Targets only large viewports

As you can see, `-m` and `-l` are appended to the class in order to target specific viewport sizes.

## Mobile-first architecture

Tachyons strictly adheres to a mobile-first architecture for a few reasons.
The primary reason is mobile performance.
Typically, smaller viewports are associated with mobile devices that are underpowered in comparison to tablet and desktop devices.
Using mobile-first media queries ensures that mobile devices have to parse as little css as possible.

If you take a look at the following Tachyons source css we can see this concept in action:

```css
/* Parsed by all devices */
.dn { display: none; }

/* Parsed by medium and large devices */
@media (--breakpoint-medium) {
  .dn-m { display: none; }
}

/* Parsed only by large devices */
@media (--breakpoint-large) {
  .dn-l { display: none; }
}
```

As you can see, mobile devices get to skip parsing 66% percent of the above css.
This is a substantial performance improvement.

Another benefit from mobile-first architecture is things become more intuitive.
It's also a lot more fun to design in the browser by composing classes to target breakpoints rather than repeatedly switching back to the css and writing new rules and media queries.

## Visibility matrix

Classes | All Devices | Medium Devices | Large Devices
------- | ----------- | -------------- | -------------
`.dn` | Hidden | Hidden | Hidden
`.dn-m` | Visible | Hidden | Hidden
`.dn-l` | Visible | Visible | Hidden
`.dn .db-l` | Hidden | Hidden | Visible
`.dn .db-m` | Hidden | Visible | Visible
`.dn .db-m .dn-l` | Hidden | Visible | Hidden