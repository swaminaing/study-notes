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
  
**Nested Routes and Layouts **
- a nested route is a URL made of multiple parts (segments)
- nested route ဆိုတာ URL တစ်ခုပါပဲ။ file-system routing ဆိုတော့ folder hierarchy အလိုက် nested route တွေ ဖြစ်လာတယ်။
- /blog ဒါဆိုရင် app/blog/page.tsx 
- folders = URL segments
- files (page, layout) = UI
**Visualizing Nested Routes **
app/
       |- page.tsx
       |- blog/ 
                   |-page.tsx
- ဒါဆိုရင် (http://localhost:3000/blog) ဒီ URL ဖြစ်လာမယ်။
**Nested Layouts **
- layouts in the folder hierachy are also nested. 
 (nested routes တွေလိုပဲ folder hierachy အလိုက်ဖြစ်လာပါတယ်)

**Creating a dynamic segment **
- page တွေအများကြီး create မယ့်အစား၊ page မှာ အများအားဖြင့် တူမယ် content လောက်ပဲပြောင်းမယ်ဆိုရင် dynamic route တွေက အသုံးဝင်ပါတယ်။ 
- Dynamic Route တွေဖန်တီးချင်ရင် square brackets ထဲထည့်ပြီးဖန်တီးပေးရပါတယ်။
- app/blog/[slug]/page.tsx ( slug မှမဟုတ်ဘူး ကြိုက်တဲ့နာမည်ပေးလို့ရပါတယ်။ just a name တစ်ခုပါ)
- app/blog/post1 
- app/blog/post2 
**Dynamic value တွေကို ဘယ်လိုဖတ်လဲ?**
- params ဆိုတာကနေ ဖတ်ပါမယ်။
- app/blog/1 
*-** export default async function BlogPostPage({
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
}***
- ဒီလိုပြန်ခေါ်သုံးပေးရပါတယ်။
- Next version 15 ကနေစပြီး params တေွက Promise တစ်ခုပြန်ပေးပါတယ်။ ဒါကြောင့် asynchronous သဘောခေါ်ပေးမှရပါမယ်။
**Multiple Dynamic Segments**
- you can have more than one dynamic segment. 
  app/shop/[category]/[product]/page.tsx

/shop/shoes/nike
/shop/phones/iphone
ဒီလိုမျိုးတွေသုံးလို့ရပါတယ်။


