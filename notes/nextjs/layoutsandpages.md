# Layouts and Pages (From Next.js Docs)

## Creating a Page

- File-system based routing (folders နဲ့ files တွေကိုသုံးပြီး routes တွေကို ဖန်တီးလို့ရ)  
- Page is a UI that is rendered on a specific route (URL path).  
  _(ဘာကိုဆိုလိုတာလည်းဆိုတော့ user တစ်ယောက်က URL တစ်ခုကို သွားတယ်ဆိုရင် သက်ဆိုင်တဲ့ Page ရဲ့ UI ကို ပြမယ်လို့ဆိုလိုတာပါ)_  
- Examples: `/` (index page), `/about` (about page)  
- **Folder name defines URL**  
  _(ဥပမာ - `app/page.tsx` ဆိုရင် `http://localhost:3000/` (index page ကိုရပါမယ်, `app` က root folder)_  
- ဒီလိုနဲ့ page တစ်ခု ဖန်တီးခြင်း ဖြစ်ပါတယ်။

## Creating a Layout

- A layout is UI that is shared between multiple pages.  
  _(layout ကို ဘယ်လိုသုံးလဲဆိုရင် Pages တွေပြောင်းတဲ့အချိန်မှာ မပြောင်းစေချင်တဲ့အရာတွေကို Layout ထဲမှာရေးထားလိုက်တာ)_  
- Example: Header, Navbar, Sidebar, Footer စတာတွေကို Layout ထဲမှာ ထည့်ရေးလိုက်ရင် Page တိုင်းမှာ ရေးစရာမလို။  
- Layout doesn't reload when changing pages  
- Layout preserves state  
- `children` props ကနေတဆင့် components တွေကို လက်ခံသင့်တယ်  
  - Children props က Layout ဒါမှမဟုတ် Pages တွေဖြစ်နိုင်တယ်

# Nested Routes and Layouts

## Nested Routes
- A nested route is a URL made of multiple parts (segments).  
- nested route ဆိုတာ URL တစ်ခုပါပဲ။ file-system routing ဆိုတော့ folder hierarchy အလိုက် nested route တွေ ဖြစ်လာတယ်။  
- `/blog` ဆိုရင် `app/blog/page.tsx` ဖြစ်တယ်  
- **folders** = URL segments  
- **files** (page, layout) = UI  

## Visualizing Nested Routes
app/
│
├─ page.tsx
├─ blog/
│ └─ page.tsx

- ဒါဆိုရင် [http://localhost:3000/blog](http://localhost:3000/blog) ဒီ URL ဖြစ်လာမယ်။  

## Nested Layouts
- Layouts in the folder hierarchy are also nested.  
- Nested layouts တွေပါ nested routes တွေအတိုင်း folder hierarchy အလိုက်ဖြစ်လာတယ်။
- 
# Creating a Dynamic Segment
- Page တွေ အများကြီး create မယ့်အစား၊ page မှာ အများအားဖြင့် တူမယ် content လောက်ပဲပြောင်းမယ်ဆိုရင် **dynamic route** တွေက အသုံးဝင်ပါတယ်။  
- Dynamic Route တွေဖန်တီးချင်ရင် **square brackets** ထဲထည့်ပြီးဖန်တီးပေးရပါတယ်။  
- Example:
- app/blog/[slug]/page.tsx
- > `slug` မှမဟုတ်ဘူး၊ ကြိုက်တဲ့နာမည်ပေးလို့ရပါတယ်၊ just a name တစ်ခုပါ။  

- URL examples:
- /app/blog/post1
- /app/blog/post2
  
## Dynamic Value တွေကို ဘယ်လိုဖတ်လဲ?
- **params** ကနေ ဖတ်ပါမယ်။  
- Example:
- app/blog/1


```ts
export default async function BlogPostPage({
  params,
}: {
  params: { slug: string };
}) {
  const { slug } = await params;
  return (
    <div>
      <h1>Blog Post: {slug}</h1>
      <p>This is the blog post page for the post with slug "{slug}".</p>
    </div>
  );
}
```
- ဒီလို ပြန်ခေါ်သုံးပေးရပါတယ်။

- Next.js version 15 ကနေစပြီး params တွေက Promise တစ်ခု ပြန်ပေးပါတယ်။ ဒါကြောင့် asynchronous သဘောဖြင့် handle လုပ်ရပါမယ်။

## Multiple Dynamic Segments

- You can have more than one dynamic segment.

Example:
- app/shop/[category]/[product]/page.tsx
- /shop/shoes/nike
- /shop/phones/iphone






