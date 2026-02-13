# THM---Gobuster-Guide-Web-Enumeration-Reconnaissance
<img width="770" height="279" alt="image" src="https://github.com/user-attachments/assets/ed5f7f17-eeca-4154-a7db-d1c6f2ff9586" />

מדריך מעשי לשימוש בכלי ה-Gobuster למטרות איסוף מידע (Reconnaissance) ובדיקות חדירות (Penetration Testing).
מדריך לשימוש ב-Gobuster: כלי לסריקה ואיסוף מידע (Reconnaissance)
Gobuster הוא כלי קוד פתוח הכתוב בשפת Go, המשמש אנשי אבטחת מידע לביצוע "מתקפות כוח גס" (Brute Force) על מנת למצוא משאבים חבויים ברשת. הוא נחשב לאחד הכלים המהירים והאמינים ביותר בשלב ה-Scanning וה-Enumeration.

1. מושגי יסוד
לפני שנצלול לפקודות, חשוב להבין שני מושגים מרכזיים:

Enumeration (מנייה): תהליך של פירוט כל המשאבים הזמינים במטרה (תיקיות, קבצים, שמות משתמש וכו').

Brute Force (כוח גס): ניסוי של כל האפשרויות מתוך רשימה מוכנה מראש (Wordlist) עד למציאת התאמה.

2. הגדרת הסביבה (Setup)
בעבודה במעבדות כמו TryHackMe, לעיתים יש להגדיר את שרת ה-DNS כדי שה-AttackBox יזהה את הדומיינים המקומיים:

עריכת הקובץ: sudo nano /etc/resolv-dnsmasq

הוספת השורה: nameserver MACHINE_IP (במקום MACHINE_IP יש לשים את הכתובת שקיבלת).

הפעלה מחדש של השירות: /etc/init.d/dnsmasq restart

<img width="929" height="827" alt="image" src="https://github.com/user-attachments/assets/64b68800-3907-4748-9baa-86450da31ef5" />


Gobuster הוא כלי חיוני בשלבי ה-Reconnaissance וה-Scanning של בדיקות חדירות. הוא מאפשר למצוא דפים, תיקיות, תתי-דומיינים ודליי אחסון בענן שאינם גלויים לעין רגילה על ידי שימוש ב-Wordlists (רשימות מילים).

תכונות עיקריות (Available Commands):
dir: מצב לסריקת ספריות וקבצים באתרים (Directory/File enumeration).

dns: גילוי תתי-דומיינים (DNS subdomain enumeration).

vhost: זיהוי מארחים וירטואליים (Virtual Hosts) על אותה כתובת IP.

fuzz: מצב Fuzzing להחלפת מילת מפתח (FUZZ) בכתובות URL, כותרות או גוף הבקשה.

s3/gcs: סריקת דליי אחסון ב-AWS ו-Google Cloud.

<img width="942" height="384" alt="image" src="https://github.com/user-attachments/assets/c2497ed4-bb54-48ab-b3a9-a2eb59b0e8cc" />
dir: מצב סריקת ספריות.

-u: כתובת היעד.

-w: נתיב לרשימת המילים.

-t 64: שימוש ב-64 תהליכונים למהירות מירבית.

