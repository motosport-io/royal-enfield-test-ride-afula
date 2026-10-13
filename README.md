# Royal Enfield – אירוע רכיבות מבחן, מוטופאן עפולה

דף נחיתה סטטי (HTML + CSS בלבד, ללא build) שמוביל לוואטסאפ של סוכן המכירות.

## מבנה
```
index.html                     הדף כולו (סגנונות וסקריפט מוטמעים)
vercel.json                    הגדרות Vercel (cache, headers)
assets/images/hero-desktop.webp       תמונת Hero רחבה (מסכים מ-768px)
assets/images/hero-mobile.webp        תמונת Hero אנכית (מובייל)
assets/images/event-poster.webp       המודעה המקורית המרובעת (לא מוצגת בדף)
assets/images/event-poster-og.jpg     אותה מודעה ב-JPG לתצוגה מקדימה בשיתוף (WhatsApp/Facebook)
assets/logos/*.png             הלוגואים (שמורים בפרויקט, לא מוצגים בדף – הם כבר חלק מהמודעה)
assets/logos/original/         הקבצים המקוריים כפי שהתקבלו
```

## הרצה מקומית
```
npx serve .
```

## פרסום ב-Vercel
לייבא את ה-Repository ב-Vercel, Framework Preset: **Other**, ללא Build Command ו-Output Directory.
אחרי הפרסום מומלץ לעדכן ב-`index.html` את `og:image` (ואת `image` ב-JSON-LD) לכתובת מלאה של הדומיין.

## Google Tag Manager ומדידת לחיצות
הדף טוען את קונטיינר GTM ‏`GTM-WRKFCVL` (קוד ב-`<head>` ו-noscript אחרי `<body>`).

כל לחיצה על כפתור וואטסאפ שולחת ל-dataLayer:
`{ event: 'whatsapp_click', cta_location: 'main' | 'sticky' }`

ההגדרות של GA4 / Meta Pixel / Google Ads נעשות בתוך GTM:
Trigger מסוג Custom Event בשם `whatsapp_click`, ו-Data Layer Variable בשם `cta_location`.
הקוד בדף לא שולח לכלים האלה ישירות, כדי למנוע ספירה כפולה.

## שינוי מספר / הודעה
הקישור נמצא פעמיים ב-`index.html` (כפתור ראשי וכפתור צף). פורמט: `https://wa.me/<מספר>?text=<הודעה מקודדת>`.
קידוד הודעה חדשה: `node -e "console.log(encodeURIComponent('ההודעה'))"`.
