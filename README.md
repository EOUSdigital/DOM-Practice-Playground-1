
# DOM 80/20 Cheat Sheet — Lesson 01

The smallest set of things you need to get real work done.

---

## 1) The idea (keep this in your head)
- **HTML** = the recipe (file you wrote)
- **DOM** = the live dish (objects you can read/change)
- Entry points: **`window`** (tab), **`document`** (page)

**Common node types:** `1` Element • `3` Text • `8` Comment • `9` Document

---

## 2) Select (grab things)
```js
document.querySelector('CSS');      // first match or null
document.querySelectorAll('CSS');   // all matches (static NodeList)
container.querySelector('CSS');     // scoped search
// Quick CSS: #id  .class  tag  [attr="val"]  parent > child
```
**80/20:** Use `querySelector/All` + scoping. Only use `getElementById` for speed/legacy.

---

## 3) Traverse (move around)
```js
el.parentElement
el.closest('.card')            // climbs up to matching ancestor
el.firstElementChild
el.lastElementChild
el.children                    // elements only (live)
el.previousElementSibling
el.nextElementSibling
```
**Tip:** Prefer the *Element* versions to avoid whitespace **Text** nodes.

---

## 4) Create & insert (add/move/remove)
```js
const p = document.createElement('p');
p.textContent = 'Hello';       // safe text
container.append(p);           // end of container
container.prepend(p);          // start of container
ref.before(p);                 // place before ref
ref.after(p);                  // place after ref

ref.remove();                  // delete ref
ref.replaceWith(p);            // swap nodes
container.replaceChildren(p);  // replace all children at once
```
**Move vs copy:** `append(existingNode)` **moves** it. To copy: `existingNode.cloneNode(true)`.

**Trusted HTML only:**
```js
el.insertAdjacentHTML('beforeend', '<em>Hot</em>'); // only if string is trusted
```

---

## 5) Edit content, classes, attributes, data, styles
```js
// Text/HTML
el.textContent = 'txt';        // safe, fast
el.innerText                    // visible text (layout-aware)
el.innerHTML = '<b>ok</b>';    // TRUSTED strings only

// Classes
el.classList.add('active', 'primary');
el.classList.remove('primary');
el.classList.toggle('open');
el.classList.replace('old', 'new');

// Attributes & data-*
el.getAttribute('aria-label');
el.setAttribute('aria-label', 'Close');
el.dataset.id = '42';          // data-id="42"
delete el.dataset.id;

// Styles (prefer classes for UI states)
Object.assign(el.style, { padding: '8px', borderRadius: '8px' });
getComputedStyle(el).display;
```

---

## 6) Safe defaults (use these unless you have a reason not to)
- **Text:** `textContent`
- **Build UI:** `createElement` + `append/prepend/before/after`
- **State:** toggle **classes** (`classList`) not inline styles
- **Find things:** `querySelector/All` + **scoping**
- **Avoid:** `innerHTML` with untrusted strings; relying on `firstChild` (text nodes)

---

## 7) 12-line daily DOM kata (type it daily)
```js
document.title = 'DOM practice';
const h = document.querySelector('h1') || document.body.firstElementChild;
const p = document.createElement('p'); p.textContent = 'Added by JS'; h?.after(p);
p.classList.add('note');
const card = document.querySelector('[data-id]') || p;
card?.parentElement?.style.outline = '2px solid lime';
const em = document.createElement('em'); em.textContent = 'Hot'; h?.after(em);
const clone = em.cloneNode(true); h?.before(clone);
document.querySelectorAll('a').forEach((a,i)=>a.dataset.index=String(i));
const box = document.createElement('div'); box.textContent = 'Top'; document.body.prepend(box);
box.after(' — done');
```
*Goal:* build muscle memory: **select → traverse → create → insert → edit → remove**.

---

## 8) Quick self-check (1 minute)
1) What’s safer for user text: `textContent` or `innerHTML`?  
2) Which inserts inside a container: `prepend` or `before`?  
3) What does `append(existingNode)` do if the node is already in the DOM?  
4) How do you find the next element sibling?

(Answers: `textContent`; `prepend`; moves it; `el.nextElementSibling`)
