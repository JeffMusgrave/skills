# Wrapping and punctuation

Where lines start, where they end, where they break and which characters they use.

## Measure (line length)

Long lines make it harder for the eye to find the start of the next line. For long-form text, keep lines between `60ch` and `75ch`. One `ch` is the width of the `0` character in the current font, so `65ch` is roughly 65 characters per line.

```tsx
// Good: scales with the font
<p className="max-w-prose">Text</p>

// Bad: fixed width ignores the font
<p className="max-w-[592px]">Text</p>
```

Tailwind's `max-w-prose` equals `65ch`, which at a `16px` body size lands around `620px` depending on the font.

## Alignment

`text-align` controls where each line starts and ends. `text-align: justify` stretches spaces until both edges line up; it can work in specific editorial layouts but avoid it in most interfaces.

## Wrapping

| Property | Use |
| --- | --- |
| `text-wrap: balance` | Distributes text evenly across multiple lines |
| `text-wrap: pretty` | Avoids leaving a single short word on the final line |
| `overflow-wrap: break-word` | Lets long words, links and IDs break before escaping the container |
| `white-space: nowrap` | Keeps labels and badges on one line where a break looks broken |

Use `balance` on headings and `pretty` on descriptions; combined they give the best outcome. In long-form text avoid forcing wrapping for the most part, it is not the most effective use of space.

## Truncation

- Single line: `text-overflow: ellipsis`, which needs `overflow: hidden` and `white-space: nowrap`.
- Multiple lines: `line-clamp` allows any number of lines before the ellipsis.

Truncation hides content. If the missing text matters, make the full value available elsewhere (tooltip or expanded view).

## Case

`text-transform` changes how case appears without changing the underlying text. Write copy naturally and control presentation with CSS, so changing presentation never requires rewriting copy.

## Smart punctuation

Keyboard characters are not always the best characters:

| Instead of | Use |
| --- | --- |
| Straight quotes `"..."` | Curly quotes that curve around the text (keep straight quotes in code) |
| Hyphen in ranges | En dash: `2010–2020` |
| Two hyphens for an aside | Em dash character |
| Three periods `...` | The single ellipsis character `…` |
| Regular space in `16 px` | `&nbsp;` so the value never breaks apart |
| Uncontrolled word breaks | `&shy;` to mark where a word may break |

## Internationalization

- Set the `lang` attribute so browsers choose the right quotes, hyphenation and pronunciation.
- Use `dir="rtl"` for right-to-left content.
- To support both directions, use logical properties everywhere a directional one exists:

```css
/* Good */
p {
  margin-inline-start: 8px;
  text-align: start;
}

/* Bad: breaks in RTL */
p {
  margin-left: 8px;
  text-align: left;
}
```

The same applies to `padding` and every other directional property.
