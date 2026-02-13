# THM---Gobuster-Guide-Web-Enumeration-Reconnaissance
<img width="770" height="279" alt="image" src="https://github.com/user-attachments/assets/ed5f7f17-eeca-4154-a7db-d1c6f2ff9586" />

🛠️ הגדרת סביבת עבודה (Setup & Connectivity)
כדי להריץ את Gobuster בהצלחה מול שרתי המעבדה של TryHackMe ממכונה וירטואלית חיצונית (כמו Kali Linux), יש לבצע את הצעדים הבאים:

1. חיבור לרשת המעבדה (VPN)
כדי שתהיה גישה לכתובות ה-IP הפנימיות, יש להתחבר באמצעות OpenVPN:

הורד את קובץ ההגדרות האישי מהאתר (סיומת .ovpn).

הרץ את הפקודה בטרמינל (השאר אותו פתוח):

Bash
sudo openvpn /path/to/your_file.ovpn
2. הגדרת זיהוי כתובות (DNS/Hosts)
מכיוון שהמכונה האישית אינה מזהה אוטומטית את הדומיינים של המעבדה, עלינו להגדיר אותם ידנית בקובץ ה-Hosts:

פתח את הקובץ לעריכה: sudo nano /etc/hosts.

הוסף את השורה הבאה (החלף את ה-IP בכתובת המכונה הפעילה):

Plaintext
10.81.140.112  www.example.thm
שמור וצא (CTRL+O, ENTER, CTRL+X).

3. אימות הגדרות ה-DNS (במידת הצורך)
במערכות מסוימות (כמו ב-AttackBox), יש לוודא ששירות ה-DNS מוגדר להפנות קודם למכונת היעד:

עריכת הקובץ: sudo nano /etc/resolv-dnsmasq.

הוספת השורה: nameserver <MACHINE_IP> כראשונה.

הפעלה מחדש של השירות: sudo /etc/init.d/dnsmasq restart.

🚀 הרצת הכלי
לאחר השלמת החיבור, ניתן להריץ את פקודת ה-Enumeration:

Bash
gobuster dir -u "http://www.example.thm/" -w /usr/share/wordlists/dirb/small.txt -t 64
דגל -u: מגדיר את כתובת ה-URL של היעד.

דגל -w: מצביע על ה-Wordlist לביצוע ה-Brute Force.

דגל -t: קובע את מספר התהליכונים (Threads) לשיפור המהירות.

<img width="952" height="726" alt="image" src="https://github.com/user-attachments/assets/b512ddde-73fb-4d3e-8f51-b08e375eec29" />


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

<img width="943" height="913" alt="image" src="https://github.com/user-attachments/assets/8fe17d7f-eb01-4af3-9a7b-9092a7d0f459" />



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

