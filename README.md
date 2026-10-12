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

## מדידת לחיצות על וואטסאפ
כל לחיצה מפעילה `trackWhatsAppClick(location)` (`main` / `sticky`) ששולחת:
- `dataLayer.push({ event: 'whatsapp_click', cta_location })` – ל-Google Tag Manager
- `gtag('event', 'whatsapp_click')` – אם GA4 מותקן
- `fbq('track', 'Contact')` – אם Meta Pixel מותקן
- `va('event', …)` – אם Vercel Analytics מותקן
- אירוע DOM בשם `whatsapp:click`

כדי להתחיל למדוד מספיק להוסיף את קוד ההטמעה של הכלי ל-`<head>`.

## שינוי מספר / הודעה
הקישור נמצא פעמיים ב-`index.html` (כפתור ראשי וכפתור צף). פורמט: `https://wa.me/<מספר>?text=<הודעה מקודדת>`.
קידוד הודעה חדשה: `node -e "console.log(encodeURIComponent('ההודעה'))"`.
