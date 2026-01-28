## Linking and Navigating (from Docs)

ဒီ Topic ကတော့ စာဖတ်ရတာများပါတယ်။

- Next.js မှာ routes တွေက default အနေနဲ့ server ပေါ်မှာပဲ run ကြပါတယ်။
  route တစ်ခုကို မပြခင် user တွေက server response တစ်ခုကို စောင့်ရပါတယ်။
  ဒီလိုကိစ္စတွေကို ဖြေရှင်းဖို့အတွက် Next.js က **Prefetching**, **Streaming**,  
  **Client-side Transitions** တွေကို support ပေးထားပါတယ်။

- Navigation တစ်ခု ဘယ်လိုအလုပ်လုပ်လဲဆိုရင်  
  **Server Rendering** နဲ့ အပေါ်က အကြောင်းအရာတွေကို သိဖို့လိုပါတယ်။
  
## Server Rendering

- **Layouts** နဲ့ **Pages** တွေက default အနေနဲ့ **React Server Components** တွေဖြစ်ကြပါတယ်။
- User တစ်ယောက်က route တစ်ခုကို visit လုပ်တဲ့အခါ  
  Server Components တွေကို **server ပေါ်မှာ run** လုပ်ပါလိမ့်မယ်။  
  အဲဒီနောက် **Server Component Payload (SCP)** တစ်ခုကို generate လုပ်ပြီး  
  browser က အဲ့ဒီ payload ကိုအခြေခံပြီး UI ကို build လုပ်ပါတယ်။

### Types of Server Rendering

Server Rendering ကို အဓိကအားဖြင့် **၂ မျိုး** ခွဲနိုင်ပါတယ်။

#### 1. Static Rendering (Pre-rendering)

- Page တစ်ခုကို build time မှာ generate လုပ်ပြီး **save / cache** ထားပါတယ်။
- နောက်ပိုင်း request တွေအတွက် cached result ကိုပဲ အသုံးပြုပါတယ်။
- Revalidation ဖြစ်တဲ့အချိန်မှသာ page ကို ပြန် generate လုပ်ပါတယ်။

#### 2. Dynamic Rendering

- Page ကို **request တစ်ခါလာတိုင်း** server ပေါ်မှာ generate လုပ်ပါတယ်။
- Data က dynamic ဖြစ်တဲ့ page တွေအတွက် အသုံးဝင်ပါတယ်။

### HTML & Server Component Payload

- Initial build အချိန်မှာပဲ **HTML** နဲ့ **Server Component Payload (SCP)** တွေကို generate လုပ်ထားပါတယ်။

### Trade-off

- Server Rendering ရဲ့ downside က  
  user က **server response ကို စောင့်ရတဲ့အတွက်** အနည်းငယ်နှေးတယ်လို့ ခံစားရနိုင်ပါတယ်။
- ဒီပြဿနာကို Next.js က  
  **Prefetching** နဲ့ **Client-side Transitions** တွေကို သုံးပြီး လျော့ချပေးထားပါတယ်။

  Server Component Payload ဆိုတာဘာလဲ? (Read more: https://nextjs.org/docs/app/getting-started/server-and-client-components#how-do-server-and-client-components-work-in-nextjs)
- Server ပေါ်မှာဆို Next Js က React APIs တွေသုံးပြီး rendering တွေလုပ်ဆောင်ပါတယ်။ 
- အဲ့ဒီမှာ Server Components တွေကို special data format, RSC Payload အနေနဲ့ပြောင်းတယ်။ RSC ဆိုတာ **compact binary representation** of the rendered React Server Component Tree. 
- အပေါ်မှာ ပြောခဲ့သလို Client Components နဲ့ RSC တွေက pre-render လုပ်တဲ့အချိန်မှာတင် generate လုပ်ပြီးပါပြီ။
   (RSC Payload ကို client ဘက်မှာ သုံးပြီး browser's DOM ကို update လုပ်ရတယ်။) 

RSC Payload ထဲမှာ ဘာတွေပါမလဲ?
- rendered result of Server Components (Component Tree Structure)
- ဘယ်နေရာမှာ ဘယ်လို run ရမယ်ဆိုတဲ့ Client Components တွေအတွက် placeholders တွေပါတယ်။ ပြီးရင် Js file တွေအတွက် သူတို့နဲ့သက်ဆိုင်တဲ့ references တွေပါတယ်။
- props from a Server Component  to a Client Component 

ဘာတွေမပါဘူးလဲဆိုရင်? 
- event handlers တွေ, Database Logic တွေမပါဘူး။ (Isn't it obvious :smile: )

( User က Link တစ်ခုကို click လုပ်မယ်ဆို full page reload မဖြစ်တော့ဘူး။ Server က Payload တစ်ခုကို browser ဆီ generate လုပ်ပေးမယ်။ ပြီးမှ ပြောင်းတဲ့အပိုင်းတွေကို updates လုပ်ပေးမယ်။

Docs ကို ဖတ်ရင်းဖတ်ရင်းနဲ့ Next.js က စိတ်ဝင်စားဖို့ကောင်းလာပါတယ်။  
အထူးသဖြင့် သူရဲ့ **features** တွေကြောင့်ပါပဲ။

## Prefetching ဆိုတာ ဘာလဲ? (from Docs)

- **Prefetching** ဆိုတာ user က route တစ်ခုကို မသွားခင်  
  အဲ့ဒီ route ကို **background မှာ ကြိုတင် load** လုပ်ထားတဲ့ process တစ်ခုဖြစ်ပါတယ်။

- ဒီလိုလုပ်ထားတဲ့အတွက် routes တွေကြား navigation က  
  **မြန်တယ်**, **ချက်ချင်းပြောင်းသလို ခံစားရတယ်**။
  ဘာကြောင့်လဲဆိုရင် `<Link />` component တွေကို render လုပ်ပြီးတာနဲ့  
  အဲ့ဒီ link နဲ့ဆိုင်တဲ့ route အတွက် လိုအပ်တဲ့ content တွေကို  
  user click မလုပ်ခင်ကတည်းက **client-side မှာ ရထားပြီးသား** ဖြစ်နေလို့ပါ။

### Static vs Dynamic Prefetching

- Route တစ်ခုကို prefetch လုပ်တဲ့ပမာဏက  
  **Static Route** လား၊ **Dynamic Route** လား ဆိုတာပေါ်မူတည်ပါတယ်။

- **Static Routes**
  - Full route ကို **အပြည့်အဝ prefetch** လုပ်ပေးပါတယ်။

- **Dynamic Routes**
  - Prefetch ကို **skip** လုပ်သွားတာဖြစ်နိုင်ပါတယ်။
  - ဒါမှမဟုတ် **partially prefetched** ဖြစ်နိုင်ပါတယ်  
    (ဥပမာ `loading.tsx / loading.js` file ရှိတဲ့အခါ)။

### Benefits

- Dynamic routes တွေကို skip လုပ်တာဖြစ်ဖြစ်  
  partially prefetch လုပ်တာဖြစ်ဖြစ်  
  **မလိုအပ်တဲ့ server-side work တွေကို မလုပ်ရတော့ဘူး**။
- အဲ့ဒါကြောင့် server load ကိုလည်း လျော့ချပေးနိုင်ပါတယ်။

### Limitation & Solution

- ဒါပေမယ့် server response ကို စောင့်ရတဲ့နေရာတွေမှာ  
  **user experience ကို ထိခိုက်နိုင်ပါတယ်**။
- အဲ့ဒီပြဿနာကို Next.js က  
  **Streaming** ကို သုံးပြီး ဖြေရှင်းပေးထားပါတယ်။

**ဒါဆို Loading.js ဒါမှမဟုတ် Loading.tsx file ဆိုတာဘာလဲ? **
- ဒီfile က special file၊ Loading UI တွေကို React ရဲ့ Suspense နဲ့ပြပေးတယ်။ 
(ကျန်တဲ့ content တွေ stream လုပ်နေတဲ့ အချိန်မှာ server ကနေ loading state တစ်ခုကို ပြပေးတယ်။)
(prefetching မပြီးသေးတဲ့အချိန်မှာ fallback UI တစ်ခုကို ပြပေးတယ်။)
- ဒီ file က Server Component ဖြစ်ပေမယ့် "use client" နဲ့ Client Component အနေနဲ့ သုံးနိုင်တယ်။ 
*- ** Loading UI components do not accept any parameters. *
-  Shared Layouts တွေမှာ interactive ဖြစ်နေဦးမယ်၊ load လုပ်ရမယ့် content တွေကလွဲရင်။

**What is Streaming?**
- streaming နဲ့ prefetching ဆိုတာ တွဲလျက်ဖြစ်နေတယ်။ 
- route တစ်ခုလုံး render လုပ်နေတာကို မစောင့်ဘဲ၊ dynamic route ရဲ့ parts တွေကို ready ဖြစ်တာနဲ့ပြတာ။ (prefetch လုပ်တာနဲ့ သဘောတရားတူတယ်)
- shared layouts တွေ loading skeletons တွေကို စောပြီး request လို့ရတယ်။

ဒါကတော့ **loading.tsx file** ကို နားလည်အောင် စမ်းထားတာပါ။

## loading.tsx / loading.js ဆိုတာဘာလဲ

- ပြရမယ့် content ကို **စောင့်နေတဲ့အချိန်** မှာ  
  `loading.js` / `loading.tsx` file က **အလိုအလျောက် ဝင်အလုပ်လုပ်** သွားပါတယ်။

- `loading.tsx` ကို အများအားဖြင့်  
  **route level** (route တစ်ခုလုံး စောင့်နေရတဲ့အချိန်) မှာ အသုံးပြုကြပါတယ်။

- `loading.tsx` က **automatically Suspense** ဖြစ်နေပြီးသားဖြစ်လို့  
  Suspense ကို ကိုယ်တိုင်ရေးစရာမလိုပါဘူး။

## Manual Control with Suspense

- Component အချို့ကိုပဲ loading state နဲ့ control လုပ်ချင်တယ်ဆိုရင်  
  `<Suspense>` ကို **manually** သုံးလို့ရပါတယ်။

- ကိုယ်စောင့်ချင်တဲ့ component ကိုပဲ Suspense ထဲထည့်နိုင်ပါတယ်။

### Example

```tsx
<>
  <h1>Dashboard</h1>

  <Suspense fallback={<p>Loading users...</p>}>
    <Users />
  </Suspense>
</>
```

- Users component က data ကို စောင့်နေရတဲ့အချိန် fallback ထဲက UI ကို ပြပေးပါလိမ့်မယ်။

### Before (Traditional React Way)

React မှာတော့ အရင်တုန်းက state တွေကို သုံးပြီး loading logic ကို ကိုယ်တိုင်ရေးရပါတယ်။

const [loading, setLoading] = useState(true)

if (loading) return <Spinner />

## What can make transitions slow?

အချက်များစွာရှိတဲ့အထဲက  
ဒီတစ်ချက်ကို notes အနေနဲ့ မှတ်ထားပါတယ် 👇

## Disabling Prefetching

- **Prefetching** က navigation ကို  
  **ပိုမြန်စေတယ်**, **ချက်ချင်းပြောင်းသလို ခံစားရစေတယ်**  
  (user experience အရ အရမ်းကောင်းပါတယ်)။

- အဲ့ဒါကြောင့်  
  “ဒါဆို routes အကုန်လုံး prefetch လုပ်လိုက်ရင် မကောင်းဘူးလား?”  
  ဆိုတဲ့ အတွေးမျိုး ဖြစ်လာနိုင်ပါတယ်။

- ဒါပေမယ့် **prefetch မလုပ်သင့်တဲ့ နေရာတွေ** လည်း ရှိပါတယ်။

### When Prefetching Can Be Bad

- ဥပမာ  
  blog post တွေအများကြီး render လုပ်ရမယ့် route (`/blog`) ကို  
  prefetch လုပ်မိခဲ့ရင်  
  **မလိုအပ်ပဲ resources တွေ အများကြီးကုန်နိုင်ပါတယ်**။

- ဘာကြောင့်လဲဆိုရင်  
  Prefetching ဆိုတာ  
  `<Link />` component နဲ့ဆိုင်တဲ့ route ကို  
  **background မှာ download ဆွဲထားတာနဲ့ တူတာကြောင့်ပါ**။

- အဲ့ဒါကြောင့်  
  မလိုအပ်တဲ့နေရာတွေမှာ  
  `prefetch={false}` ပေးထားသင့်ပါတယ်။

```tsx
<Link href="/blog" prefetch={false}>
  Blog
</Link>
```
## Should We Disable Prefetching Everywhere?

**မဟုတ်ပါဘူး**

Prefetching ကို  
**လိုအပ်တဲ့နေရာတွေမှာတော့ ဆက်ပြီး သုံးရပါမယ်။**

## Best Practice

- အကောင်းဆုံး solution ကတော့  
  **user က link ကို hover လုပ်တဲ့အချိန်မှာမှ prefetch လုပ်ပေးတာပါ**။

- User တစ်ယောက်က link ကို hover လုပ်တဲ့အခါ  
  အဲ့ဒီ moment မှာပဲ  
  **prefetch state ကို `true` ပြန်ပေးလိုက်ရပါမယ်**။

### Benefits

➡️ ဒီလိုလုပ်ရင်

- မလိုအပ်တဲ့ download တွေကို ရှောင်နိုင်တယ်
- UX ကလည်း မနှေးသွားဘူး
