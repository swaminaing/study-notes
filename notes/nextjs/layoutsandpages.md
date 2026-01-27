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
