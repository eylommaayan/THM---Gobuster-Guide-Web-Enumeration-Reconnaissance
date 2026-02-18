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
<img width="943" height="913" alt="image" src="https://github.com/user-attachments/assets/8fe17d7f-eb01-4af3-9a7b-9092a7d0f459" />

Bash
gobuster dir -u "http://www.example.thm/" -w /usr/share/wordlists/dirb/small.txt -t 64
דגל -u: מגדיר את כתובת ה-URL של היעד.

דגל -w: מצביע על ה-Wordlist לביצוע ה-Brute Force.

דגל -t: קובע את מספר התהליכונים (Threads) לשיפור המהירות.




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




פתרון המעבדה (מבוסס על התמונות שלך)
לפי הצילומים ששלחת, כך הגעת לפתרון:

איזה דגל מוסיפים כדי לדלג על אימות TLS?

תשובה: --no-tls-validation.

סריקת האתר www.offensivetools.thm:

פקודת הסריקה:
gobuster dir -u "http://www.offensivetools.thm" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt.

הספרייה שמשכה את תשומת הלב בתוצאות: secret.

מציאת הדגל בתוך קובץ JS:

ביצוע סריקה בתוך ספריית secret עם סיומת .js:
gobuster dir -u "http://www.offensivetools.thm/secret" -w ... -x .js

נמצא קובץ בשם flag.js.

קריאת הקובץ: curl http://www.offensivetools.thm/secret/flag.js.

הדגל: THM{ReconWasASuccess}.
<img width="1867" height="889" alt="image" src="https://github.com/user-attachments/assets/edb30fa3-8d29-4d37-b5b5-3db11275489f" />


הנה החלק האחרון למדריך ה-GitHub שלך, המתמקד בסריקת תתי-דומיינים (Subdomain Enumeration). חלק זה משלים את המדריך ונותן תמונה מלאה על השימוש ב-Gobuster.

---

# 🌐 Gobuster: גילוי תתי-דומיינים (Subdomain Enumeration)

בנוסף לסריקת ספריות, Gobuster מאפשר לבצע Brute Force על רשומות DNS כדי לגלות תתי-דומיינים חבויים. זהו שלב קריטי מכיוון שתתי-דומיינים (כמו `dev.example.com`) עשויים להכיל פגיעויות שלא קיימות בדומיין הראשי.

## 🛠 מצב DNS - דגלים מרכזיים

כדי לעבוד במצב זה, נשתמש במילת המפתח `dns`.

| דגל קצר | דגל ארוך | תיאור |
| --- | --- | --- |
| **`-d`** | `--domain` | **(חובה)** דומיין היעד שאותו נרצה לסרוק. |
| **`-w`** | `--wordlist` | **(חובה)** נתיב לרשימת המילים. |
| `-i` | `--show-ips` | הצגת כתובות ה-IP שאליהן מפנים תתי-הדומיינים שנמצאו. |
| `-c` | `--show-cname` | הצגת רשומות CNAME (לא ניתן לשילוב עם `-i`). |
| `-r` | `--resolver` | שימוש בשרת DNS ספציפי לביצוע השאילתות. |

---

## 🚀 פקודות הרצה

### סריקת תתי-דומיינים בסיסית:

```bash
gobuster dns -d offensivetools.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt

```

### הסבר על הפעולה:

Gobuster לוקח כל מילה מרשימת המילים ומנסה לבנות שאילתת DNS. למשל, אם המילה היא `shop`, הכלי ינסה לגשת לכתובת `shop.offensivetools.thm`.

---

## ❓ תשובות לתרגול (TryHackMe)

* **מלבד מילת המפתח `dns` והדגל `-w`, איזה דגל קצר חובה להוסיף?**
* תשובה: **`-d`**.


* **כמה תתי-דומיינים מוגדרים עבור הדומיין `offensivetools.thm`?**
* תשובה: **`4`**.


<img width="1654" height="746" alt="image" src="https://github.com/user-attachments/assets/8d73b6db-03d9-47a4-b0f5-e035ee231585" />
*

הנה המדריך המתורגם והמסוכם עבור מצב **Vhost Enumeration** ב-Gobuster, מותאם להעלאה ל-GitHub:

---

# 🌐 Gobuster: גילוי מארחים וירטואליים (Vhost Enumeration)

מצב ה-**vhost** הוא הכלי האחרון שנלמד ב-Gobuster. הוא מאפשר לבצע Brute Force כדי לגלות מארחים וירטואליים (Virtual Hosts).

### מהם מארחים וירטואליים?

אלו הם אתרים שונים המאוחסנים על אותה מכונה פיזית. למרות שהם עשויים להיראות כמו תתי-דומיינים, יש הבדל טכני:

* **Subdomains:** מוגדרים ב-DNS.
* **Virtual Hosts:** מבוססי IP ורצים על אותו שרת. מצב זה סורק על ידי שילוב שם המארח (Hostname) עם רשימת מילים ובדיקת ה-URL שנוצר.

---

## 🛠 דגלים נפוצים (Flags)

| דגל קצר | דגל ארוך | תיאור |
| --- | --- | --- |
| `-u` | `--url` | כתובת ה-URL הבסיסית (דומיין היעד). |
|  | `--append-domain` | מצמיד את דומיין הבסיס לכל מילה ברשימה (למשל: `word.example.com`). |
| `-m` | `--method` | מגדיר את שיטת ה-HTTP (למשל GET או POST). |
|  | `--domain` | מוסיף דומיין לכל ערך ברשימה ליצירת שם מארח תקין. |
|  | `--exclude-length` | מסנן תוצאות לפי אורך גוף התגובה (שימושי לניקוי "רעש"). |
| `-r` | `--follow-redirect` | מעקב אחר הפניות HTTP. |

---

## 🚀 איך להשתמש במצב vhost?

התחביר הבסיסי דורש את הדגלים `-u` ו-`-w`:

```bash
gobuster vhost -u "http://example.thm" -w /path/to/wordlist

```

### דוגמה מעשית ומורכבת:

בבדיקות מציאותיות, לעיתים נצטרך פקודה מפורטת יותר כדי להתמודד עם תשתיות ללא DNS מוגדר במלואו:

```bash
gobuster vhost -u "http://10.10.x.x" --domain example.thm -w /usr/share/wordlists/... --append-domain --exclude-length 250-320

```

**מדוע להשתמש ב-`--exclude-length`?**
בסריקות כאלו מתקבלות הרבה תוצאות "חיוביות כוזבות" (False Positives). רובן יהיו בעלות גודל תגובה זהה (למשל דפי שגיאה 404). סינון האורך מאפשר לנו לראות רק את התוצאות הרלוונטיות, בדרך כלל אלו עם סטטוס **200 OK**.

---

## 🔍 ניתוח הבקשה (HTTP Host Header)

Gobuster פועל על ידי שליחת בקשות HTTP ושינוי שדה ה-**Host** בכל פעם:

* **www**: החלק שמוחלף על ידי רשימת המילים.
* **.example.thm**: הדומיין המוגדר דרך דגל `--domain`.

---

## ❓ תשובות לתרגול (TryHackMe)

* **כמה Vhosts בדומיין `offensivetools.thm` מחזירים קוד סטטוס 200?**
* **תשובה:** יש להריץ את הפקודה על היעד ולספור את התוצאות עם סטטוס 200. לפי הדוגמה בחדר, התשובה היא **4**.

<img width="1896" height="826" alt="image" src="https://github.com/user-attachments/assets/f1e0bd87-7d1b-4db3-8d19-9c0062f2ff67" />


---
*
